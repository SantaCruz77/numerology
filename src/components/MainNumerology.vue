<script setup>
import { ref } from "vue";

const nameRef = ref("");
const nameListRef = ref([]);
const ls = localStorage.nameList;

nameListRef.element = ls ? JSON.parse(ls) : [];

let aaa = [];

const cal = (value) => {
  aaa = [];
  value = value.toUpperCase();
  let valueArray = value.split("");
  for (let index = 0; index < valueArray.length; index++) {
    if (
      (valueArray[index] === "A") |
      (valueArray[index] === "J") |
      (valueArray[index] === "S")
    ) {
      aaa.push(1);
    }
    if (
      (valueArray[index] === "B") |
      (valueArray[index] === "K") |
      (valueArray[index] === "T")
    ) {
      aaa.push(2);
    }
    if (
      (valueArray[index] === "C") |
      (valueArray[index] === "L") |
      (valueArray[index] === "U")
    ) {
      aaa.push(3);
    }
    if (
      (valueArray[index] === "D") |
      (valueArray[index] === "M") |
      (valueArray[index] === "V")
    ) {
      aaa.push(4);
    }
    if (
      (valueArray[index] === "E") |
      (valueArray[index] === "N") |
      (valueArray[index] === "W")
    ) {
      aaa.push(5);
    }
    if (
      (valueArray[index] === "F") |
      (valueArray[index] === "O") |
      (valueArray[index] === "X")
    ) {
      aaa.push(6);
    }
    if (
      (valueArray[index] === "G") |
      (valueArray[index] === "P") |
      (valueArray[index] === "Y")
    ) {
      aaa.push(7);
    }
    if (
      (valueArray[index] === "H") |
      (valueArray[index] === "Q") |
      (valueArray[index] === "Z")
    ) {
      aaa.push(8);
    }
    if ((valueArray[index] === "I") | (valueArray[index] === "R")) {
      aaa.push(9);
    }
  }
  return aaa.reduce(
    (accumulator, currentValue) => accumulator + currentValue,
    0
  );
};

const setName = () => {
  const id = new Date().getTime();
  const calculatedName = cal(nameRef.value);
  console.log(calculatedName);
  nameListRef.value.push({
    id: id,
    name: calculatedName,
  });
  localStorage.nameList = JSON.stringify(nameListRef.value);
  nameRef.value = "";
};

const deleteName = (id) => {
  const name = nameListRef.value.find((name) => name.id === id);
  const idx = nameListRef.value.findIndex((name) => name.id === id);

  const delMsg = "「" + name.name + "」を削除しますか？";
  if (!confirm(delMsg)) return;

  nameListRef.value.splice(idx, 1);
  localStorage.nameList = JSON.stringify(nameListRef.value);
};
</script>

<template>
  <div class="wrapper">
    <div class="aaa">
      <input
        type="text"
        v-model="nameRef"
        class="input"
        placeholder="入力してください"
      />
      <button class="btn-submit" @click="setName">送信</button><br />
    </div>
    <div v-for="data in nameListRef" :key="data.id">
      <div class="bbb">
        <div class="todo">
          <label>{{ data.name }}</label>
        </div>
        <button class="btn-delete" @click="deleteName(data.id)">削除</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 10px;
}
.input {
  border: 1px solid #ccc;
  border-radius: 6px;
  width: 300px;
  padding: 0px 12px;
  font-size: 16px;
  height: 50px;
}
.todo {
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 12px;
  width: 300px;
}

.aaa {
  margin-bottom: 20px;
}
.bbb {
  display: flex;
  padding-top: 3px;
  height: 50px;
}
.btn-submit {
  background: green;
  margin-left: 10px;
  font-weight: bold;
  height: 50px;
}
.btn-delete {
  background: limegreen;
  margin-left: 10px;
  font-weight: bold;
}
</style>
