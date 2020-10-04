<template>
  <header id="Header" class="header">
    <HeaderNavTop />
    <SubHeader />
  </header>
</template>

<script>
import HeaderNavTop from "./header-top.vue";
import SubHeader from "./header-bottom.vue";
export default {
  name: "Header",
  components: {
    HeaderNavTop,
    SubHeader
  },
  data: () => {
    return {};
  },
};
</script>