<template>
  <section class="src-components-nav-bar">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <router-link to="/formulario">
        <a class="navbar-brand" href="#">Formulario</a>
      </router-link>
      <router-link to="/tabla">
        <a class="navbar-brand" href="#">Tabla</a>
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
    </nav>
  </section>
</template>

<script>
export default {
  name: "src-components-nav-bar",
  props: [],
  mounted() {},
  data() {
    return {};
  },
  methods: {},
  computed: {},
};
</script>

<style scoped lang="css">
.src-components-nav-bar {
}
</style>
