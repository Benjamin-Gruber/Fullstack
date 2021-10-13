<template>
  <v-container fluid class="d-flex flex-wrap" justify-center>
    <CarCard class="mx-8 my-4" :c="c" v-for="c of cars" :key="c" @buyCar="buyCar" />
  </v-container>
</template>

<script>
import CarCard from '@/components/CarCard.vue';
import axios from 'axios';

export default {
  props: {
    cars: {
      type: Array,
    },
  },

  components: {
    CarCard,
  },

  methods: {
    async buyCar(c) {
      await axios({
        url: 'http://localhost:3000/cars/' + c.id,
        method: 'PATCH',
        contentType: 'application/json',
        data: {
          title: c.title + ' RESERVED',
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
