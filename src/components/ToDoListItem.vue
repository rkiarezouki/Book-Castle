<script setup>
const props = defineProps(['livre'])
const emit = defineEmits(["deleteL, decrementL, incrementL"]);
</script>

<template>
    <li>
        <h3>le titre est: {{ livre.titre }}</h3>
        <h3>la quantité est: {{ livre.qtestock }}</h3>
        <h3>Le prix est: {{ livre.prix }}</h3>
        <button @click="$emit('deleteL', livre.id)">Supprimer</button>
        <button @click="$emit('incrementL', livre)">+1</button>
        <button @click="$emit('decrementL', props.livre)">-1</button>
        
        
    </li>

</template>

<style scoped>

li{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: aliceblue;
    margin: 20px;
    border-radius: 1vw;
    opacity: 0.8;
    font-family: 'MagicSchoolOne';

}
button{
 border-radius: 6px; 
  cursor: pointer; 
  background-color: #853677; /* couleur de fond */
  font-family: 'MagicSchoolOne';
}

@font-face {
  font-family: 'MagicSchoolOne';
  src: url('/public/MagicSchoolOne.ttf');
}


</style>