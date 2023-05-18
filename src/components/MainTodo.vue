<script setup>
import { ref } from "vue";
const nameRef = ref("");
const nameListRef = ref([]);

const cal = () => {
  const id = new Date().getTime();
  nameListRef.value.push({ id: id, name: nameRef.value });
  localStorage.nameList = JSON.stringify(nameListRef.value);
  nameRef = "";
};
</script>

<template>
  <input type="text" v-model="nameRef" placeholder="入力してください" />
  <button @click="cal">送信</button><br />
  {{ todoRef }}
</template>
