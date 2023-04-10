<template>
  <div>
    <v-container>
      <v-card class="text-center pa-4">
        <h2>วันนี้</h2>
        <v-btn color="green" block outline @click="goToDetail(alldays)">Click</v-btn>
      </v-card>
      <div class="mt-4">
        <v-row>
          <v-col cols="6" v-for="n in reversedNumbers" :key="n">
            <v-card class="text-center elevation-5" @click="goToDetail(n)">
              <div class="my-16">{{ n }}</div>
            </v-card>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </div>
</template>

<script setup></script>

<script>
export default {
  data() {
    return {
      alldays: 9,
    };
  },
  methods: {
    goToDetail(day) {
      console.log("test");
      this.$router.push({ path: "/detail", query: { day } });
      console.log(this);
    },
  },
  computed: {
    reversedNumbers() {
      let numbers = [];
      for (let i = this.alldays; i >= 1; i--) {
        numbers.push(i);
      }
      return numbers;
    },
  },
};
</script>
