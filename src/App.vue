<template>
  <navbar-component
    :pages="pages"
    :active-page="activePage"
    :change-link="changeLink"
  ></navbar-component>
  <page-component :page="pages[activePage]"></page-component>
</template>

<script>
import NavbarComponent from "@/components/NavbarComponent.vue";
import PageComponent from "@/components/PageComponent.vue";

export default {
  components: {
    NavbarComponent,
    PageComponent,
  },
  created() {
    this.getPages();
  },
  data() {
    return {
      activePage: 0,
      // useDarkNavbar: true,
      pages: [],
    };
  },
  methods: {
    changeLink(index) {
      this.activePage = index;
    },
    async getPages() {
      const pages = await fetch("pages.json");
      this.pages = await pages.json();
    },
  },
};
</script>
