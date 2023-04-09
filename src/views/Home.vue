<template>
  <div>
    <v-container>
      <v-card class="text-center pa-4">
        <h2>วันนี้</h2>
        <v-btn block  outline  color="#FFF2CC" @click="goToDetail">Click</v-btn>
      </v-card>
    </v-container>
  </div>
</template>

<script setup>
</script>

<script>
export default {
  methods:{
    goToDetail(){
      console.log('test')
      this.$router.push('/detail')
      console.log(this)
    }
  }
}
</script>
