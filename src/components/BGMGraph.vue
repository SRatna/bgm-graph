<template>
  <div>
    <div class="graph-cotainer">
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
        <polygon
          v-if="showResult"
          :points="finalPoints"
          fill="#8686fc"
          stroke="black"
          stroke-width="1"
        />
        <template v-for="n in 6">
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
      </svg>
      <template v-for="n in 6">
        <span :class="legendClasses[n - 1]" :key="'legend' + n">
          {{ legends[n - 1] }}
        </span>
      </template>
    </div>
    <div style="padding-top: 32px">
      <template v-for="n in 6">
        <div class="input-container" :key="'input' + n">
          <label>{{ legends[n - 1] }}</label>
          <input type="number" min="1" max="4" v-model="values[n - 1]" />
        </div>
      </template>
    </div>
    <button style="padding: 8px; margin: 16px" @click="onSubmit">
      See Result
    </button>
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
      legends: ["one", "two", "three", "four", "five", "six"],
      legendClasses: ["one", "two", "three", "four", "five", "six"],
      values: [1, 1, 1, 1, 1, 1],
      showResult: false,
      finalPoints: "",
    };
  },
  computed: {
    center() {
      return this.length / 2;
    },
    labelX() {
      return this.center - this.labelXOffset;
    },
  },
  methods: {
    getLinePoints(lineNum, pointNum) {
      const angle = ((90 - (lineNum - 1) * 60) * Math.PI) / 180;
      const distanceX = this.distance90 * Math.cos(angle);
      const distanceY = this.distance90 * Math.sin(angle);
      return {
        x: this.center + distanceX * pointNum,
        y: this.center - distanceY * pointNum,
      };
    },
    labelY(pointNum) {
      return this.center - pointNum * this.distance90 + this.labelYOffset;
    },
    onSubmit() {
      const points = [];
      this.values.forEach((value, index) => {
        const point = this.getLinePoints(index + 1, value * 1);
        points.push(point.x);
        points.push(point.y);
      });
      this.showResult = true;
      this.finalPoints = points.join(",");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.graph-cotainer {
  position: absolute;
  margin-left: 200px;
}
.graph-cotainer .one {
  position: absolute;
  left: 236px;
  top: 25px;
}
.graph-cotainer .two {
  position: absolute;
  left: 435px;
  top: 135px;
}
.graph-cotainer .three {
  position: absolute;
  left: 435px;
  top: 345px;
}
.graph-cotainer .four {
  position: absolute;
  left: 236px;
  top: 455px;
}
.graph-cotainer .five {
  position: absolute;
  left: 40px;
  top: 345px;
}
.graph-cotainer .six {
  position: absolute;
  left: 50px;
  top: 135px;
}
.input-container {
  padding: 8px;
}
.input-container label {
  width: 55px;
  display: inline-block;
}
</style>
