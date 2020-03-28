<template>
    <a-layout-footer :style="{ textAlign: 'center' }">
      Bu uygulama Covid19 virüsünün ülkeler üzerindeki etkileri ile ilgili verileri anlık olarak sunmak için yazılmıştır. Her hakkı saklıdır&nbsp;&copy;&nbsp;{{ new Date().getFullYear() }}
      <div>
        Written By Hüseyin GÖZTOK => <a target="_blank" href="https://www.linkedin.com/in/huseyingoztok/">Linkedin</a>
      </div>
    </a-layout-footer>
</template>

<script>
import { Layout } from 'ant-design-vue';
const Footer = Layout.Footer;
export default {
  components: {
    "a-layout-footer": Footer,
  }
}
</script>