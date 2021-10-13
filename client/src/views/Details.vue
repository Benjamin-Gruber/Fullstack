<template>
  <v-app>
    <v-main>
      <LogoBar />
      <v-container justify-center class="d-flex">
        <div>
          <v-card class="mx-auto my-7" max-width="450">
            <v-img height="350" :src="car.image"></v-img>

            <v-card-title
              ><span class="font-weight-bold text-center">{{ car.title }}</span></v-card-title
            >

            <v-simple-table>
              <thead>
                <tr>
                  <th>Price</th>
                  <th>Miles</th>
                  <th>Year of Make</th>
                  <th>Current Owner</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>{{ car.price }}</td>
                  <td>{{ car.miles }}</td>
                  <td>{{ car.yearOfMake }}</td>
                  <td>{{ car.owner.firstName }} {{ car.owner.lastName }}</td>
                </tr>
              </tbody>
            </v-simple-table>
            <p class="ml-5 mr-4 grey--text">{{ car.description }}</p>

            <v-card-actions>
              <v-btn to="/" class="white--text purple darken-1" flat value="feed">
                <span>GO BACK</span>
              </v-btn>

              <v-btn color="error" class="red darken-2" @click="orderCar()" v-if="car.status === 'available'">
                ORDER CAR
              </v-btn>
            </v-card-actions>
          </v-card>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import LogoBar from '@/components/LogoBar.vue';
import axios from 'axios';

export default {
  data() {
    return {
      car: [],
    };
  },

  created() {
    this.getCar(this.id);
  },

  props: {
    id: {
      type: Number,
    },
  },

  methods: {
    async getCar(id) {
      try {
        const { data } = await axios({
          url: `http://localhost:3000/cars/${id}`,
          method: 'GET',
        });
        this.car = data;
      } catch (error) {
        console.error(error);
      }
    },

    async orderCar() {
      try {
        // this.car.title = this.car.title + ' *RESERVED*'; Damit es direkt Updated (bleibt nicht gespeicher) 
        await axios({
          url: `http://localhost:3000/cars/${this.car.id}`,
          method: 'PATCH',
          contentType: 'application/json',
          data: {
            title: this.car.title + ' *RESERVED*',
            status: 'reserved',
          },
        });
      } catch (error) {
        console.error(error);
      }
    },
  },

  components: {
    LogoBar,
  },
};
</script>

<style lang="scss" scoped></style>
