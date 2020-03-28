<template>
  <a-skeleton active :loading="loading">
    <a-table :columns="columns" :dataSource="filteredCountryList" rowKey="key">
      <a slot="name" slot-scope="text">{{text}}</a>
      <span slot="customNewDeaths">
        <a-icon type="frown-o" />&nbsp;New Deaths
      </span>
      <span slot="customTotalDeaths">
        <a-icon type="frown-o" />&nbsp;
        <a-icon type="frown-o" />&nbsp;Total Deaths
      </span>
      <span slot="NewConfirmed" slot-scope="NewConfirmed" v-if="NewConfirmed > 0">
        <a-tag color="orange">{{NewConfirmed}}</a-tag>
      </span>
      <span
        slot="TotalConfirmed"
        slot-scope="TotalConfirmed"
        v-if="TotalConfirmed > 0"
      >{{TotalConfirmed}}</span>
      <span slot="NewDeaths" slot-scope="NewDeaths" v-if="NewDeaths > 0">
        <a-tag color="#dc3545">{{NewDeaths}}</a-tag>
      </span>
      <span slot="TotalDeaths" slot-scope="TotalDeaths" v-if="TotalDeaths > 0">{{TotalDeaths}}</span>
      <span slot="NewRecovered" slot-scope="NewRecovered" v-if="NewRecovered > 0">{{NewRecovered}}</span>
      <span
        slot="TotalRecovered"
        slot-scope="TotalRecovered"
        v-if="TotalRecovered > 0"
      >{{TotalRecovered}}</span>
    </a-table>
  </a-skeleton>
</template>

<script>
import { Table, Tag, Skeleton, Icon } from "ant-design-vue";
export default {
  components: {
    "a-table": Table,
    "a-tag": Tag,
    "a-skeleton": Skeleton,
    "a-icon": Icon
  },
  data() {
    return {
      countries: [],
      loading: true,
      sortDirections: ["descend", "ascend"]
    };
  },
  props: {
    search: String
  },
  computed: {
    columns() {
      const columns = [
        {
          title: "Country",
          dataIndex: "Country",
          key: "Country",
          sorter: (a, b) => a.Country.localeCompare(b.Country),
          sortDirections: this.sortDirections
        },
        {
          title: "New Confirmed",
          dataIndex: "NewConfirmed",
          key: "NewConfirmed",
          scopedSlots: { customRender: "NewConfirmed" },
          sorter: (a, b) => a.NewConfirmed - b.NewConfirmed,
          sortDirections: this.sortDirections
        },
        {
          title: "Total Confirmed",
          dataIndex: "TotalConfirmed",
          key: "TotalConfirmed",
          scopedSlots: { customRender: "TotalConfirmed" },
          sorter: (a, b) => a.TotalConfirmed - b.TotalConfirmed,
          sortDirections: this.sortDirections
        },
        {
          key: "NewDeaths",
          dataIndex: "NewDeaths",
          scopedSlots: { customRender: "NewDeaths" },
          slots: { title: "customNewDeaths" },
          sorter: (a, b) => a.NewDeaths - b.NewDeaths,
          sortDirections: this.sortDirections
        },
        {
          key: "TotalDeaths",
          dataIndex: "TotalDeaths",
          scopedSlots: { customRender: "TotalDeaths" },
          slots: { title: "customTotalDeaths" },
          sorter: (a, b) => a.TotalDeaths - b.TotalDeaths,
          sortDirections: this.sortDirections
        },
        {
          title: "New Recovered",
          key: "NewRecovered",
          dataIndex: "NewRecovered",
          scopedSlots: { customRender: "NewRecovered" },
          sorter: (a, b) => a.NewRecovered - b.NewRecovered,
          sortDirections: this.sortDirections
        },
        {
          title: "Total Recovered",
          key: "TotalRecovered",
          dataIndex: "TotalRecovered",
          scopedSlots: { customRender: "TotalRecovered" },
          sorter: (a, b) => a.TotalRecovered - b.TotalRecovered,
          sortDirections: this.sortDirections
        }
      ];
      return columns;
    },
    filteredCountryList() {
      return this.countries.filter(c => {
        return c.Country.toLowerCase().includes(this.search);
      });
    }
  },
  created() {
    fetch("https://api.covid19api.com/summary")
      .then(response => {
        return response.json();
      })
      .then(response => {
        this.countries = response.Countries.filter(c => c.Country !== "");
        for (let i = 0; i < this.countries.length; i++) {
          this.countries[i].key = `${i + 1}`;
        }
        this.loading = false;
      });
  }
};
</script>