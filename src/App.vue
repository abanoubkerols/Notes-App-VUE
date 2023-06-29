<script setup>
import { ref } from 'vue';
const showModel = ref(false)
const newNote = ref("")
const notes = ref([])
const error = ref("")

function getRandomColor(){
 let color = "hsl(" + Math.random() * 360 + " , 100% , 75%)"
  return color
}

const addNotes = ()=>{
  if(newNote.value.length < 10 ){
    return error.value= "Note must be at least 10 character or more "
  }
  notes.value.push({
    id:Math.floor(Math.random()*1000000),
    text : newNote.value,
    date : new Date(),
    bgColor: getRandomColor()
  })

  showModel.value = false
  newNote.value = ""
  error.value = " "
}

</script>




<template>
  <main>

    <div v-if="showModel" class="overlay">
      <div class="model">
        <textarea v-model.trim="newNote" name="notes" id="notes" cols="30" rows="10"></textarea>
        <p  v-if="error">{{ error }}</p>
        <button @click="addNotes">Add Notes</button>
        <button @click="showModel = false" class="close">close</button>
      </div>
    </div>


    <div class="container">
      <header>
        <h1>Notes </h1>
        <button @click="showModel = true">+</button>
      </header>
      <div class="card-container">
        <div v-for="note in notes" class="card" :key="note.id"  :style="{backgroundColor:note.bgColor}">
          <p class="main-text">{{ note.text }}.</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
        
      </div>
    </div>
  </main>
</template>

<style scoped>
*,
body,
html {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}


.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

h1 {

  font-size: 4rem;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  border-radius: 50%;
  background-color: rgb(22, 21, 21);
  color: #fff;
  font-size: 2rem;
  line-height: 1;


}

.card-container {
  display: flex;
  flex-wrap: wrap;
  /* justify-content: space-between; */
  /* margin: 50px ; */
}

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(204, 212, 81);
  display: flex;
  border-radius: 10px;
  justify-content: space-between;
  flex-direction: column;
  margin-right: 20px;
  margin-top: 20px;
  padding: 10px;
}

.date {
  font-size: 1rem;
  font-weight: bolder;




}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  background-color: rgb(0, 0, 0, 0.5);
  z-index: 11;
  display: flex;
  align-items: center;
  justify-content: center;
}

.model {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.model button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: #fff;
  cursor: pointer;
  margin-top: 15px;
}

textarea {
  resize: none;
}

.model .close {
  background-color: rgb(160, 46, 46);
  margin-top: 20px;
}
.model p{
  color: red;
  margin-top: 5px;
}
</style>