<script setup>
// @ts-nocheck

import { ref } from "vue";

const nums = ref("");

const btn = (n) => {
  if (nums.value === "") {
    nums.value = n;
  } else {
    nums.value += n;
  }
};
const clear = () => {
  nums.value = "";
};
const calc = (m) => {
  if (nums.value === "" || nums.value === "*") {
    if (m == "-") {
      nums.value = m;
      return;
    } else {
      return;
    }
  }
  nums.value += m;
};
const evalFunc = () => {
  nums.value = eval(nums.value);
};
</script>

<template>
  <div class="wrap">
    <div class="calc">
      <div class="display">{{ nums }}</div>
      <div class="grid">
        <div class="flex">
          <div class="btn" @click="clear">C</div>
          <div class="btn" @click="evalFunc">=</div>
        </div>
        <div class="row">
          <div class="flex col">
            <div class="btn" @click="calc('+')">+</div>
            <div class="btn" @click="calc('-')">-</div>
            <div class="btn" @click="calc('*')">x</div>
            <div class="btn" @click="calc('/')">/</div>
          </div>
          <div class="flex-wrap">
            <div class="btn" @click="btn('1')">1</div>
            <div class="btn" @click="btn('2')">2</div>
            <div class="btn" @click="btn('3')">3</div>
            <div class="btn" @click="btn('4')">4</div>
            <div class="btn" @click="btn('5')">5</div>
            <div class="btn" @click="btn('6')">6</div>
            <div class="btn" @click="btn('7')">7</div>
            <div class="btn" @click="btn('8')">8</div>
            <div class="btn" @click="btn('9')">9</div>
            <div class="btn" @click="btn('0')">0</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.wrap {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.calc {
  max-width: 500px;
  width: 100%;
  font-family: Arial, sans-serif;
  font-weight: 600;
  user-select: none;
}
.display {
  width: 100%;
  height: 200px;
  padding: 20px;
  background-color: ghostwhite;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  border: 1px solid lightblue;
  font-size: 36px;
  word-break: break-all;
}
.flex-wrap {
  display: flex;
  flex-wrap: wrap;
}
.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.row {
  display: flex;
  flex-direction: row-reverse;
}
.col {
  flex-direction: column;
}
.grid {
  background-color: aquamarine;
}
.btn {
  border: 1px solid lightblue;
  font-size: 28px;
  width: 125px;
  height: 70px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  color: #050505;
}
.btn:hover {
  background-color: white;
}
</style>
