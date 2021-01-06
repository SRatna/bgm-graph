<template>
  <div>
    <svg :height="length" :width="length">
      <template v-for="n in 4">
        <circle
          :cx="center"
          :cy="center"
          :r="distance90 * n"
          fill="none"
          stroke="black"
          stroke-width="2"
          :key="'circle' + n"
        />
      </template>
      <template v-for="n in 8">
        <line
          :x1="center"
          :y1="center"
          :x2="getLinePoints(n, 4).x"
          :y2="getLinePoints(n, 4).y"
          fill="none"
          stroke="black"
          stroke-width="2"
          :key="'line' + n"
        />
      </template>
      <template v-for="n in 4">
        <text :x="labelX" :y="labelY(n)" fill="black" :key="'label' + n">
          {{ n }}
        </text>
      </template>
      <!-- 
      <circle cx="108" cy="108" r="5" fill="black" /> -->
    </svg>
  </div>
</template>

<script>
export default {
  name: "BGMGraph",
  data: function () {
    return {
      length: 500,
      distance90: 50,
      labelXOffset: 12, // this depends on text size
      labelYOffset: 18,
    };
  },
  computed: {
    center() {
      return this.length / 2;
    },
    distance45() {
      return this.distance90 / Math.sqrt(2);
    },
    labelX() {
      return this.center - this.labelXOffset;
    },
  },
  methods: {
    getLinePoints(lineNum, pointNum) {
      switch (lineNum) {
        case 1 || "one": {
          return {
            x: this.center + this.distance90 * pointNum,
            y: this.center,
          };
        }
        case 2 || "two": {
          return {
            x: this.center + this.distance45 * pointNum,
            y: this.center - this.distance45 * pointNum,
          };
        }
        case 3 || "three": {
          return {
            x: this.center,
            y: this.center - this.distance90 * pointNum,
          };
        }
        case 4 || "four": {
          return {
            x: this.center - this.distance45 * pointNum,
            y: this.center - this.distance45 * pointNum,
          };
        }
        case 5 || "five": {
          return {
            x: this.center - this.distance90 * pointNum,
            y: this.center,
          };
        }
        case 6 || "six": {
          return {
            x: this.center - this.distance45 * pointNum,
            y: this.center + this.distance45 * pointNum,
          };
        }
        case 7 || "seven": {
          return {
            x: this.center,
            y: this.center + this.distance90 * pointNum,
          };
        }
        case 8 || "eight": {
          return {
            x: this.center + this.distance45 * pointNum,
            y: this.center + this.distance45 * pointNum,
          };
        }
      }
    },
    labelY(pointNum) {
      return this.center - pointNum * this.distance90 + this.labelYOffset;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
