<template>
  <v-app>
    <LogoBar />
    <CarCards :cars="cars" />
  </v-app>
</template>

<script>
import LogoBar from '@/components/LogoBar.vue';
import CarCards from '@/components/CarCards.vue';
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      cars: [],
    };
  },

  components: {
    LogoBar,
    CarCards,
  },

  created() {
    this.getCars();
  },

  methods: {
    async getCars() {
      try {
        const { data } = await axios({
          url: 'http://localhost:3000/cars',
          method: 'GET',
        });
        this.cars = data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
