<template>
  <div class="nav-bar">
    <b-navbar class="p-3">
      <b-navbar-toggle target="nav-text-collapse"></b-navbar-toggle>

      <b-navbar-brand href="https://conucowormfarm.com"
        >
        <img
          src="../assets/logoTwo.png"
          alt=""
          id="logo"
          class="img-fluid"
      />
      <!-- Home -->
      </b-navbar-brand>

      <!-- <b-collapse id="nav-text-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/">Home</b-nav-item>
        </b-navbar-nav>
      </b-collapse> -->
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#logo {
  max-width: 192px;
}

.nav-link{
  color: #333;
  font-size: 18px;
}
</style>
