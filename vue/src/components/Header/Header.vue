<template>
  <a-layout-header :style="{ position: 'fixed', zIndex: 1, width: '100%' }">
    <div class="logo"> ABİS TEKNOLOJİ</div>
    <a-menu
      theme="dark"
      mode="horizontal"
      :defaultSelectedKeys="['2']"
      :style="{ lineHeight: '64px' }"
    >
    </a-menu>
  </a-layout-header>
</template>

<script>
import { Layout, Menu } from "ant-design-vue";
const Header = Layout.Header;
export default {
  components: {
    "a-menu": Menu,
    "a-layout-header": Header
  }
};
</script>

<style scoped>
.logo {
  width: 120px;
  height: 31px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px 24px 16px 0;
  float: left;
  color: white;
  text-align: center;
  line-height: 31px;
}
</style>