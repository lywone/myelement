<template>
  <div id="app" :class="classObj">
    <div v-if="showNav" :class="{ 'fixed-header': fixedHeader }">
      <navbar />
    </div>
    <router-view style="padding-top: 60px; height: 100%; overflow: auto" />
  </div>
</template>

<script>
import { Navbar } from "./layout/components";
import { mapState } from "vuex";
export default {
  name: "App",
  components: {
    Navbar,
  },
  computed: {
    ...mapState({
      sidebar: (state) => state.app.sidebar,
      device: (state) => state.app.device,
      fixedHeader: (state) => state.settings.fixedHeader,
    }),
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        openSidebar: this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === "mobile",
      };
    },
    showNav() {
      const { path } = this.$route;
      return path !== "/login";
    },
  },
};
</script>
<style lang="scss" scoped>
.fixed-header {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 9;
  width: 100%;
  transition: width 0.28s;
}

.hideSidebar .fixed-header {
  width: 100%;
}

.mobile .fixed-header {
  width: 100%;
}
</style>
