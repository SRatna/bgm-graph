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
      </svg>
      <template v-for="n in 8">
        <span :class="legendClasses[n - 1]" :key="'legend' + n">
          {{ legends[n - 1] }}
        </span>
      </template>
    </div>
    <div style="padding-top: 32px">
      <template v-for="n in 8">
        <div class="input-container" :key="'input' + n">
          <label>{{ legends[n - 1] }}</label>
          <input type="number" min="1" max="4" v-model="values[n - 1]" />
        </div>
      </template>
    </div>
    <button style="padding: 8px; margin: 16px" @click="onSubmit">See Result</button>
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
      legends: ["one", "two", "three", "four", "five", "six", "seven", "eight"],
      legendClasses: [
        "one",
        "two",
        "three",
        "four",
        "five",
        "six",
        "seven",
        "eight",
      ],
      values: [1, 1, 1, 1, 1, 1, 1, 1],
      showResult: false,
      finalPoints: "",
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
        case 1: {
          return {
            x: this.center + this.distance90 * pointNum,
            y: this.center,
          };
        }
        case 2: {
          return {
            x: this.center + this.distance45 * pointNum,
            y: this.center - this.distance45 * pointNum,
          };
        }
        case 3: {
          return {
            x: this.center,
            y: this.center - this.distance90 * pointNum,
          };
        }
        case 4: {
          return {
            x: this.center - this.distance45 * pointNum,
            y: this.center - this.distance45 * pointNum,
          };
        }
        case 5: {
          return {
            x: this.center - this.distance90 * pointNum,
            y: this.center,
          };
        }
        case 6: {
          return {
            x: this.center - this.distance45 * pointNum,
            y: this.center + this.distance45 * pointNum,
          };
        }
        case 7: {
          return {
            x: this.center,
            y: this.center + this.distance90 * pointNum,
          };
        }
        case 8: {
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
  left: 460px;
  top: 240px;
}
.graph-cotainer .two {
  position: absolute;
  left: 400px;
  top: 90px;
}
.graph-cotainer .three {
  position: absolute;
  left: 230px;
  top: 25px;
}
.graph-cotainer .four {
  position: absolute;
  left: 75px;
  top: 90px;
}
.graph-cotainer .five {
  position: absolute;
  left: 15px;
  top: 240px;
}
.graph-cotainer .six {
  position: absolute;
  left: 80px;
  top: 390px;
}
.graph-cotainer .seven {
  position: absolute;
  left: 230px;
  top: 455px;
}
.graph-cotainer .eight {
  position: absolute;
  left: 395px;
  top: 390px;
}
.input-container {
  padding: 8px;
}
.input-container label {
  width: 55px;
  display: inline-block;
}
</style>
