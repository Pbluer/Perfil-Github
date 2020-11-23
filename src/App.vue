<template>
  <v-app>
    <v-main>
      <HelloWorld :search="searchProfile"/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    searchProfile:''
  }),
};
</script>
