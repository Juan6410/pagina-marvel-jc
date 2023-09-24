<template>
  <v-card>
    <v-tabs style="background-color: black; color: azure;">
      <nuxt-link style="color: aliceblue;" v-for="item in items" :key="item.tab" :to="item.route">
        <v-tab>{{ item.tab }}</v-tab>
      </nuxt-link>
    </v-tabs>
    <router-view></router-view>
  </v-card>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      tab: null,
      items: [
        { tab: "Inicio", route: "/" },
        { tab: "Personajes", route: "/heroes" },
      ],
    };
  },
};
</script>
