<template>
  <nav
    id="nav"
    class="navbar navbar-expand-lg"
    :class="[
      'navbar',
      'navbar-expand-lg',
      `navbar-${this.theme}`,
      `bg-${this.theme}`,
    ]"
  >
    <div class="container">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="container-fluid d-flex justify-content-between">
          <div class="navbar-nav">
            <nav-link-component
              class="hoverable"
              v-for="(page, index) in pages"
              :key="index"
              :page="page"
              :change-link="changeLink"
              :is-active="index === activePage"
              @click.prevent="changeLink(index)"
            >
            </nav-link-component>
          </div>
          <div class="button-container">
            <button class="btn btn-primary" @click="changeTheme()">
              Go {{ theme === "light" ? "dark" : "light" }}
            </button>
            <div
              class="changeThemeNotif"
              :class="{ show: changeThemeIsClicked }"
            >
              <p>You have changed to {{ theme }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import NavLinkComponent from "@/components/NavLinkComponent.vue";
export default {
  components: {
    NavLinkComponent,
  },
  props: ["pages", "activePage", "changeLink"],
  data() {
    return {
      theme: "dark",
      changeThemeIsClicked: false,
    };
  },
  methods: {
    changeTheme() {
      this.theme = this.theme === "light" ? "dark" : "light";
      // this.changeThemeIsClicked = false;
      this.changeThemeIsClicked = true;
      setTimeout(() => {
        this.changeThemeIsClicked = false;
      }, 2000);
    },
  },
};
</script>

<style scoped>
.button-container {
  position: relative;
}
.changeThemeNotif {
  box-shadow: 7px 8px 47px 0 rgba(100, 100, 100, 0.43);
  position: absolute;
  left: -100%;
  width: 300%;
  padding: 10px;
  background: white;
  border-radius: 10px;
  text-align: center;
  opacity: 0;
}

.show {
  animation-name: show-change-theme-notif;
  animation-duration: 800ms;
  animation-iteration-count: 2;
  animation-direction: alternate;
}

@keyframes show-change-theme-notif {
  from {
    opacity: 0;
    top: 200%;
  }
  to {
    opacity: 1;
    top: 100%;
  }
}
</style>
