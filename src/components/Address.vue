<template>
  <div class="header" @click="open">
    <span class="item id">{{ id }}</span>
    <span class="item address">
      <span>{{ location }}</span>
      <span>{{ place }}</span>
    </span>
    <span class="item labels" >
      <span v-for="label in labels" :key="label">{{ label }}</span>
    </span>
    <span class="item prop">{{ proper }}</span>
    <span class="item phone">{{ phone }}</span>
  </div>
</template>

<script>
import $ from 'jquery'
export default {
    /* eslint-disable */
    name: 'Address',
  props : [ 'id', 'location', 'place', 'labels', 'proper', 'phone' ],
  emits: [ 'update'],
  methods : {
      open(){
        $(".form").toggleClass("active");
        this.$emit('update', this.id)
      }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>