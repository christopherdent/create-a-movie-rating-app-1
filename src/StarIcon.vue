<template>
    <button @click="toggleStar" :class="starClass"></button>
  </template>
  
  <script>
  export default {
    props: {
      clicked: Boolean,
      index: Number,
    },
    data() {
      return {
        isClicked: this.clicked,
      };
    },
    methods: {
      toggleStar(a) {
        console.log(this.index)
        this.isClicked = !this.isClicked;
        this.$emit('toggle', this.isClicked);
      },
    },
    computed: {
      starClass() {
        return this.isClicked ? 'star-clicked' : 'star-unclicked';
      },





    },
  };
  </script>
  