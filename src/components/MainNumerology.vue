<script setup>
import { ref } from "vue";
const nameRef = ref("");
const nameListRef = ref([]);
const ls = localStorage.nameList;
nameListRef.value = ls ? JSON.parse(ls) : [];

const cal = () => {
  const id = new Date().getTime();
  nameListRef.value.push({ id: id, name: nameRef.value });
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
      <button class="btn-submit" @click="cal">送信</button><br />
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
