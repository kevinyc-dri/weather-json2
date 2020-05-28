// Weather.vue

<template>
	<div class="demo">
    <h3>{{title}}</h3>
    <h3 v-for='name in names' :key='name.id'>{{name}}</h3>
    <hr>
    <!-- <input type="text" v-model='demotext'> -->
    <input type="number" v-model='num1'>
    <input type="number" v-model='num2'>

    <hr>
    <!-- {{demotext}} -->
    {{addition}} 
    <hr>
    <!-- <button @click='cleardemotext()'>clear</button> -->
  </div>
</template>

<script>
export default {
	name: 'Demo',
	data() { // mutable
    return {
      demotext:'anything',
      num1: 0,
      num2: 0,

    };
  },

  props: {
    title: { type:String },
    names: { type: Array, default: ()=> [] }
  },


  watch: {
    
  },

  methods: {
    cleardemotext() {
      this.demotext=''; 
    }
  },

  computed: {
    addition() {
      return parseInt(this.num1) + parseInt(this.num2);
		}
  },

  mounted() {
  },
  
};
</script>


