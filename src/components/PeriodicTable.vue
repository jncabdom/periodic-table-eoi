<template>
  <div class="periodic-table">
    <div class="elements-container" v-for="(el, index) in elements" :key="index">
      <div v-if="index === 1" class="col-16"></div>
      <Element :element="el"></Element>
    </div>
  </div>
</template>

<script>

import Element from "./Element.vue";

export default {
  name: "PeriodicTable",
  mounted() {
    this.getElements();
  },
  data() {
    return {
      elements: []
    };
  },
  components: {
    Element
  },
  methods: {
    getElements() {
      fetch("/data/table-data.json")
        .then(response => response.json())
        .then(data => (this.elements = data));
    }
  }
};
</script>

<style>
.periodic-table {
  display: grid;
  grid-template-columns: repeat(18, 1fr);
  grid-template-rows: repeat(8, 1fr);
  border: 2px grey;
}
</style>
