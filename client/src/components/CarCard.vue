<template>
  <div>
    <v-card class="mx-auto" max-width="344">
      <v-img height="250" :src="c.image"></v-img>
      <v-card-title>{{ c.title }}</v-card-title>
      <v-card-text>
        Owner: <span class="font-weight-black">{{ c.owner.firstName }} {{ c.owner.lastName }}</span> <br />
        <br />
        Year: <span class="font-weight-black">{{ c.yearOfMake }}</span> <br />
        Miles: <span class="font-weight-black">{{ c.miles }}</span> <br /><br />
        <span v-if="c.status === 'available'"
          >Price: <span class="font-weight-black">{{ c.price }}</span></span
        >
        <br /><br />
        <span v-if="c.status === 'reserved'">Price: <span class="font-weight-black">N/A</span></span>
        <br /><br />
        <br />

        <v-btn
          @click="toDetails(c.id)"
          v-if="c.status === 'available'"
          :cars="c"
          class="white--text purple darken-1"
          flat
          value="feed"
        >
          <span>DETAILS</span>
        </v-btn>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    c: {
      type: Object,
    },
  },
  methods: {
    buyCar() {
      this.$emit('buyCar', this.c);
    },
    toDetails(id) {
      this.$router.push(`/details/${id}`);
    },
  },
};
</script>

<style lang="scss" scoped></style>
