<template>
  <a-layout style="min-height: 100vh" id="components-layout-demo-top" class="layout">
    <app-header />
    <a-layout-content :style="{ padding: '0 50px', marginTop: '100px' }">
      <div :style="{ background: '#fff', minHeight: '380px' }">
        <div :style="{ padding: '24px' }">
          <a-row>
            <a-col :span="12">
              <a-input placeholder="Search ..." @change="onSearch">
                <a-icon slot="addonAfter" type="search" />
              </a-input>
            </a-col>
          </a-row>
        </div>
        <countries-table :search="search" />
      </div>
    </a-layout-content>
    <app-footer />
  </a-layout>
</template>

<script>
import Header from "../Header/Header";
import Footer from "../Footer/Footer";
import CountriesTable from "../../scenes/Countries/CountriesTable";
import { Layout, Icon, Input, Row, Col } from "ant-design-vue";
const { Content } = Layout;
export default {
  components: {
    "app-footer": Footer,
    "app-header": Header,
    "a-layout": Layout,
    "a-layout-content": Content,
    "a-icon": Icon,
    "a-input": Input,
    "a-row": Row,
    "a-col": Col,
    "countries-table": CountriesTable
  },
  data() {
    return {
      search: ""
    };
  },
  methods: {
    onSearch(e) {
      this.search = e.target.value.toLowerCase();
    }
  }
};
</script>

<style>
.ant-table-pagination.ant-pagination {
  margin: 16px 16px 16px 0;
}
</style>