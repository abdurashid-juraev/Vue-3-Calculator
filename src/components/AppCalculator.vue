<template>
  <div class="mt-10 text-white">
    <div class="w-1/3 mx-auto bg-zinc-900 rounded-xl px-3 py-4">
      <div
        class="h-40 w-full px-4 pt-7 mb-2 outline outline-2 text-2xl break-all text-ellipsis rounded-md outline-slate-700"
      >
        {{ prevNumber }} {{ selectedOperation }} {{ currentNumber }}
      </div>
      <div class="grid grid-cols-4 gap-2">
        <button
          @click="clear"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          C
        </button>
        <button
          @click="backspace"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          x
        </button>
        <button
          @click="btn('%')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          %
        </button>
        <button
          @click="btn('/')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          /
        </button>
        <button
          @click="btn('1')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          1
        </button>
        <button
          @click="btn('2')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          2
        </button>
        <button
          @click="btn('3')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          3
        </button>
        <button
          @click="btn('*')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          *
        </button>
        <button
          @click="btn('4')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          4
        </button>
        <button
          @click="btn('5')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          5
        </button>
        <button
          @click="btn('6')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          6
        </button>
        <button
          @click="btn('-')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          -
        </button>
        <button
          @click="btn('7')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          7
        </button>
        <button
          @click="btn('8')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          8
        </button>
        <button
          @click="btn('9')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          9
        </button>
        <button
          @click="btn('+')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          +
        </button>
        <button
          @click="btn('0')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-700"
        >
          0
        </button>
        <button
          @click="minusValue"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          +/-
        </button>
        <button
          @click="btn('.')"
          class="hover:bg-slate-600 duration-150 rounded-md text-3xl py-4 bg-slate-800"
        >
          .
        </button>
        <button
          @click="btn('=')"
          class="hover:bg-blue-500 duration-150 rounded-md text-3xl py-4 bg-blue-600"
        >
          =
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
// @ts-nocheck

import { ref, onMounted } from "vue";
const data = [];
const btn = (value) => {
  if (value === "=" || value === "Enter") {
    data.push({
      operations: `${prevNumber.value} ${selectedOperation.value} ${currentNumber.value}`,
      plus: eval(
        `${prevNumber.value} ${selectedOperation.value} ${currentNumber.value}`
      ),
    });

    calculate();
  } else if (value === "%") precentage();
  else if (operations.includes(value)) applyOperation(value);
  else if (numbers.includes(value)) appendNumber(value);
  console.log(data);
};
const operations = ["+", "-", "*", "/"];
const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
const currentNumber = ref("");
const prevNumber = ref("");
const selectedOperation = ref("");
const total = ref("");
const calculate = () => {
  if (selectedOperation.value === "+") plus();
  else if (selectedOperation.value === "-") minus();
  else if (selectedOperation.value === "*") multiply();
  else if (selectedOperation.value === "/") divide();
  else if (selectedOperation.value === "%") precentage();
  prevNumber.value = "";
  selectedOperation.value = "";
};
const appendNumber = (value) => {
  currentNumber.value = currentNumber.value + value;
};
const applyOperation = (value) => {
  calculate();
  prevNumber.value = currentNumber.value;
  currentNumber.value = "";
  selectedOperation.value = value;
};
const plus = () => {
  currentNumber.value = +prevNumber.value + +currentNumber.value;
  total.value = currentNumber.value;
};
const minus = () => {
  currentNumber.value = prevNumber.value - currentNumber.value;
  total.value = currentNumber.value;
};
const multiply = () => {
  currentNumber.value = prevNumber.value * currentNumber.value;
  total.value = currentNumber.value;
};
const divide = () => {
  currentNumber.value = prevNumber.value / currentNumber.value;
  total.value = currentNumber.value;
};
const precentage = () => {
  currentNumber.value = currentNumber.value / 100;
  total.value = currentNumber.value;
};
const backspace = () => {
  if (currentNumber.value.length !== 0 && currentNumber.value !== "0") {
    currentNumber.value = currentNumber.value.slice(0, -1);
  }
};
const clear = () => {
  (currentNumber.value = ""),
    (selectedOperation.value = ""),
    (prevNumber.value = "");
};
const minusValue = () => {
  if (currentNumber.value === "0") {
    return (currentNumber.value = "-0");
  }
  if (currentNumber.value === "-") {
    return (currentNumber.value = "0");
  }
  if (currentNumber.value === "0.") {
    return (currentNumber.value = `-${currentNumber.value}`);
  }
  if (currentNumber.value === "-0.") {
    return (currentNumber.value = "0.");
  }
  currentNumber.value = `${currentNumber.value * -1}`;
};
const handleKeydown = (e) => {
  btn(e.key);
};
onMounted(() => window.addEventListener("keydown", handleKeydown));
</script>
