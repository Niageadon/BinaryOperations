<template>
<div>
  <v-container grid-list-md text-xs-center>
    <v-layout row wrap>

      <v-flex xs12>
        <h1>First register</h1>
      </v-flex>

      <v-flex v-for="(num, id) in firstRegisterByte" :key="id" xs1>
        <v-card v-on:click="firstRegisterByte[id].val ^= 1" :color="num.color">
          <v-card-text  class="px-0">{{num.val}}</v-card-text>
          <v-divider></v-divider>
          <div style="background-color: #4188D2">{{num.weight}}</div>
        </v-card>
      </v-flex>
      <v-flex xs2>
        <v-card  color="#0D58A6" class="px-0">
          <v-card-text>{{firstRegisterValue}} </v-card-text>
          <div style="background-color: #4188D2">&#8721</div>
        </v-card>
      </v-flex>

    </v-layout>

  </v-container>

</div>
</template>

<script>
  export default {
    name: "ContentPage",

    data(){
      return{
        //https://colorscheme.ru/#0b320w0w0w0w0
        firstRegisterByte: [
          {id: 0, val: 0, weight: 128, color: '#BF5030'},
          {id: 1, val: 0, weight: 64, color: '#BF5030'},
          {id: 2, val: 0, weight: 32, color: '#BF5030'},
          {id: 3, val: 0, weight: 16, color: '#BF5030'},
          {id: 4, val: 0, weight: 8, color: '#BF5030'},
          {id: 5, val: 0, weight: 4, color: '#BF5030'},
          {id: 6, val: 0, weight: 2, color: '#BF5030'},
          {id: 7, val: 0, weight: 1, color: '#BF5030'},
        ],
        firstRegisterValue: firstRegisterByte[1].val,
      }
    },

    computed: {
      changeCardColor: function () {
        return 1
      }


    },

    methods:{
      setBit(){

      }
    }
  }
</script>

<style scoped>

</style>
