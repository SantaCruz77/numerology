<script setup>
import { ref } from "vue";

const nameRef = ref("");
const nameListRef = ref(getStoredNameList());

const getStoredNameList = () => {
  const storedList = localStorage.getItem("nameList");
  return storedList ? JSON.parse(storedList) : [];
};

const storeNameList = () => {
  localStorage.setItem("nameList", JSON.stringify(nameListRef.element));
};

const calculateName = (element) => {
  return element * 3;
};

const addName = () => {
  const id = new Date().getTime();
  const calculatedName = calculateName(nameRef.element);
  nameListRef.element.push({ id, name: calculatedName });
  storeNameList();
  nameRef.element = "";
};

const deleteName = (id) => {
  const nameIndex = nameListRef.element.findIndex((name) => name.id === id);
  const nameToDelete = nameListRef.element[nameIndex];

  if (confirm(`「${nameToDelete.name}」を削除しますか？`)) {
    nameListRef.element.splice(nameIndex, 1);
    storeNameList();
  }
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
