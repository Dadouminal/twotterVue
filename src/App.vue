<template>
  <div id="app">
    <nav class="navbar is-danger">
      <div class="navbar-brand">
        <a href="#" class="navbar-item">Twotter</a>
        <div class="navbar-menu">
          <div class="navbar-end">
            <a href="#" class="navbar-item">Dadouminal</a>
          </div>
        </div>
      </div>
    </nav>
    <UserProfile />
  </div>
</template>

<script>
import UserProfile from "./components/UserProfile.vue";
export default {
  name: "App",
  components: {
    UserProfile,
  },
};
</script>

<style></style>
