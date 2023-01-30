<template>
  <v-app>
    <v-main class="main-backgroind-gradient">
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>

<style scoped>
.main-backgroind-gradient {
  background: rgb(1, 187, 224);
  background: linear-gradient(
    90deg,
    rgba(1, 187, 224, 1) 20%,
    rgba(3, 150, 201, 1) 50%,
    rgba(7, 95, 153, 1) 85%
  );
}
</style>
