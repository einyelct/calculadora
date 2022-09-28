<template>
  <!-- Happy Coding -->
  <div class="p-3 bodyCalculator">
    <div class="w-full rounded m-1 p-2 numbers-color numbers-result text-end">
      {{ calculatorOperation || 0 }}
    </div>
    <div class="w-full rounded m-1 p-2 numbers-color numbers-result text-end">
      {{ calculatorValues }}
    </div>

    <!-- Calculator buttons -->
    <b-row>
      <div class="col-3" v-for="operator in calculatorElements" :key="operator">
        <button
          class="w-100 text-white text-center m-1 py-2 numbers-color rounded"
          :class="{
            'button-operator': ['C', '*', '/', '-', '+', '%', '='].includes(operator),
          }"
          @click="action(operator)"
        >
          {{ operator }}
        </button>
      </div>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      calculatorOperation:'',
      operator: null,
      previousCalculatorValue: "",
    };
  },
  computed: {
    calculatorValues() {
      if (this.calculatorValue) {
        return this.calculatorValue;
      } else {
        return 0;
      }
    },
  },
  methods: {
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
        this.calculatorOperation = this.calculatorOperation + ""+ n;
        
      }
      if (n === "C") {
        this.calculatorValue = "";
        this.calculatorOperation = '';
      }
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
        this.calculatorOperation =this.calculatorOperation + ''+ n;
      }
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style scoped>
.bodyCalculator {
  max-width: 400px;
  margin: 50px auto;
  background: #234;
}
.numbers-color {
  background: #2f8df1;
}
.numbers-result{
    font-weight: bolder;
}
button:hover {
  cursor: pointer;
  background: #3d5875;
}
.button-operator {
  background: #3fb984;
}
</style>
