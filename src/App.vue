<script setup>
import ToDoHeader from "./components/ToDoHeader.vue";
import ToDoList from "./components/ToDoList.vue";
</script>

<template>
  <div id="A1">
    <ToDoHeader />
    <ToDoList />
  </div>
</template>

<style scoped>
@font-face {
  font-family: 'MagicSchoolOne';
  src: url('/public/MagicSchoolOne.ttf');
}

div#A1 {

  background-image: url('./src/assets/Harry2.jpg');
  background-color: #F1E8C4;
  font-family: 'MagicSchoolOne', sans-serif;
  background-repeat: no-repeat;
  background-position: center;

}
</style>
