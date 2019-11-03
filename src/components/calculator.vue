<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div v-on:click="clc" class="btn grey" id="black">AC</div>
    <div v-on:click="sign" class="btn grey" id="black">+/-</div>
    <div v-on:click="percent" class="btn grey" id="black">%</div>
    <div v-on:click="divide" class="orange btn">÷</div>
    <div v-on:click="append('7')" class="dark-grey btn active">7</div>
    <div v-on:click="append('8')" class="dark-grey btn">8</div>
    <div v-on:click="append('9')" class="dark-grey btn">9</div>
    <div v-on:click="multiply" class="orange btn">x</div>
    <div v-on:click="append('4')" class="dark-grey btn">4</div>
    <div v-on:click="append('5')" class="dark-grey btn">5</div>
    <div v-on:click="append('6')" class="dark-grey btn">6</div>
    <div v-on:click="minus" class="orange btn">-</div>
    <div v-on:click="append('1')" class="dark-grey btn">1</div>
    <div v-on:click="append('2')" class="dark-grey btn">2</div>
    <div v-on:click="append('3')" class="dark-grey btn">3</div>
    <div v-on:click="plus" class="orange btn">+</div>
    <div v-on:click="append('0')" class="dark-grey zero">0</div>
    <div v-on:click="dot" class="dark-grey btn">.</div>
    <div v-on:click="equal" class="orange btn">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clc() {
      this.current = "";
    },
    sign() {
      //when +/- press
      if (this.current.charAt(0) === "-" || this.current === "") {
        //check number is there - at front
        this.current = this.current.slice(1); //if - exist remove it
      } else {
        this.current = "-" + this.current; //else add -
      }
    },
    percent() {
      this.current = this.current / 100;
    },
    append(number) {
      //if true just use this.operatorClicked
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = this.current + number;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      );
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");
.calculator {
  margin: 0 auto;
  width: 400px;
  font-family: sans-serif;
  font-size: 40px;
  display: grid;
  background-color: black;
  padding: 8px;
  border-radius: 10px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.calculator div {
  display: flex;
  align-items: center;
  justify-content: center;
  /* text-align: center; */
  border-style: solid;
  margin: 8px;
  height: 85px;
  width: 85px;
  color: #fff;
  /* line-height: 78px; */
  cursor: pointer;
  border: 2px;
  -webkit-box-shadow: 0px 0px 76px -20px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 0px 0px 76px -20px rgba(0, 0, 0, 0.75);
  box-shadow: 0px 0px 76px -20px rgba(0, 0, 0, 0.75);
}
div.display {
  grid-column: 1 / 5;
  color: white;
  width: 373px;
  font-size: 98px;
  text-align: right;
  overflow: hidden;
  justify-content: right;
}
div.zero {
  grid-column: 1 / 3;
  width: 182px;
  height: 85px;
  border-radius: 35px;
}
.orange {
  background-color: #ff9900;
  transition: 0.3s;
}
.grey {
  background-color: #999999;
}
#black {
  color: #0d0d0d;
}
.dark-grey {
  background-color: #333333;
}
.btn {
  border-radius: 50%;
}
div.orange:hover {
  background-color: #fff;
  color: #ff9900;
}
/* .active:active {
  background-color: #ff9900;
  color: #fff;
} */
</style>
