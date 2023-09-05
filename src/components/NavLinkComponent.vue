<script>
export default {
  props: ["page", "isActive"],
};
</script>

<template>
  <span class="nav-container">
    <a
      class="nav-item nav-link"
      :class="{ 'active emphasize': isActive }"
      :href="page.link.url"
      :title="`Ini link menuju halaman ${page.link.title}`"
      >{{ page.link.title }}</a
    >
    <div class="nav-dropdown">
      <p>Menu pertama</p>
      <p>Menu kedua</p>
      <p>Menu ketiga</p>
    </div>
  </span>
</template>

<style scoped>
.emphasize {
  text-decoration: underline;
}
.nav-container {
  position: relative;
}
.nav-dropdown {
  background: #1c1c1b;
  padding: 10px;
  position: absolute;
  opacity: 0;
  color: white;
  border-radius: 10px;
}
.nav-container:hover .nav-dropdown {
  animation-name: fade-up-nav-dropdown;
  animation-duration: 300ms;
  animation-iteration-count: 1;
  animation-fill-mode: forwards;
}

@keyframes fade-up-nav-dropdown {
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
