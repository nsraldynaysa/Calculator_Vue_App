<template>
  <div class="calculator">
    <div class="display">{{ current === current ? `${current}` : ''}}</div>
    <div @click="clear"  class="btn operator-one">C</div>
    <div @click="sign"  class="btn operator-one">+/-</div>
    <div @click="percent" class="btn operator-one">%</div>
    <div @click="divide"  class="btn operator-two">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator-two">×</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus"  class="btn operator-two">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator-two">+</div>
    <div @click="append('0')" class="btn-zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator-two">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
        )}`;
        this.previous = null;
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  background-color: white; /* #e1f5fe */
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; 
}
.calculator {
  margin: 0 auto;
  bottom: 2%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(75px, auto);
  font-size: 30px;
  text-align: center;
}
.display {
  height: 200px;
  line-height: 200px;
  text-align: center;
  grid-column: 1 / 5;
  color:#333;
}
.btn-zero {
  grid-column: 1 / 3;
  margin: 5px;
  line-height: 75px;
  background-color: cornsilk;
  border-radius: 16px;
  cursor: pointer;
   /* box-shadow: 60px -30px -30px #00ffff, 50px 20px 20px #00d2c6; */

}
.btn {
  margin: 5px;
  width: 75px;
  height: 75px;
  line-height: 75px;
  background-color: cornsilk;
  border-radius: 16px;
  cursor: pointer;
   /* box-shadow: 60px -30px -30px #00ffff, 50px 20px 20px #00d2c6; */
}
.operator-one {
  background-color: darkgray;
}
.operator-two {
  background-color: crimson;
  color: white;
}
</style>
