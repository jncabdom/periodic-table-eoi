<template>
  <div @mouseenter="hover" @mouseleave="hover" class="element" :style="info">
    <div class="at-number-container">
      <div class="at-number">{{ element["atomicNumber"] }}</div>
    </div>
    <div class="symbol">{{ element["symbol"] }}</div>
    <div :style="getColor" class="name">{{ element["name"] }}</div>
    <div :style="getColor" class="at-mass">{{ atMass }}</div>
  </div>
</template>

<script>

export default {
  name: "Element",
  props: {
    element: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      active: false,
      info: {
        backgroundColor: "#" + this.element.cpkHexColor
      },
      hidden: {
        opacity: 0
      },
      shown: {
        opacity: 1
      }
    };
  },
  methods: {
    hover() {
      this.active = !this.active;
    }
  },
  computed: {
    getColor() {
      return this.active ? this.shown : this.hidden;
    },
    atMass() {
      let result = this.element.atomicMass;
      if (typeof result === "string") {
        const position = result.indexOf("(");
        if (position !== -1) {
          result = result.substr(0, position);
        }
        result = parseFloat(result).toFixed(2);
        return result;
      } else return result[0];
    }
  }
};
</script>

<style scoped>
.element:hover {
  transform: scale(1.25);
  z-index: 10;
}

.name,
.at-mass {
  transition: opacity 0.5s;
}
.element {
  width: 5rem;
  color: black;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: transform 0.25s;
}
.symbol {
  font-size: 2rem;
}

.at-number-container {
  width: 100%;
  display: flex;
  justify-content: left;
  align-items: left;
}
</style>
