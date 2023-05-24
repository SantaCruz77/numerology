<script setup>
import { ref } from "vue";

const nameRef = ref("");
const nameListRef = ref([]);
const ls = localStorage.nameList;

nameListRef.element = ls ? JSON.parse(ls) : [];

const cal = (value) => {
  value = value.toUpperCase();
  let valueArray = value.split("");
  return valueArray;
  // for (let index = 0; index < valueArray.length; index++) {
  //   const element = valueArray[index];

  //   if ((element === "A") | (element === "J") | (element === "S")) {
  //     element = 1;
  //   }
  //   if ((element === "B") | (element === "K") | (element === "T")) {
  //     element = 2;
  //   }
  //   if ((element === "C") | (element === "L") | (element === "U")) {
  //     element = 3;
  //   }
  //   if ((element === "D") | (element === "M") | (element === "V")) {
  //     element = 4;
  //   }
  //   if ((element === "E") | (element === "N") | (element === "W")) {
  //     element = 5;
  //   }
  //   if ((element === "F") | (element === "O") | (element === "X")) {
  //     element = 6;
  //   }
  //   if ((element === "G") | (element === "P") | (element === "Y")) {
  //     element = 7;
  //   }
  //   if ((element === "H") | (element === "Q") | (element === "Z")) {
  //     element = 8;
  //   }
  //   if ((element === "I") | (element === "R")) {
  //     element = 9;
  //   }
  //   return element;
  // }
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
