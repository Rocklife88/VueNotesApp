
<script setup>
import{ref} from "vue";


// states
const showModal= ref(false)
const newNote= ref("")
const notes= ref([])
const errorMessage=ref("")


function getRandomColor() {
  let color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}


const addNote = () => {
  if(newNote.value.length <10) {
return errorMessage.value="note needs to be 10 characters or more"

  }
  notes.value.push({
    text:newNote.value,
    date: new Date(),
    id: Math.floor(Math.random()*100000),
    backgroundColor:getRandomColor()

  })
  showModal.value=false;
  newNote.value="";
  errorMessage.value= "";
}




</script>



<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{errorMessage}}</p>
        <button @click="addNote"  class="modal-btn">Add note</button>
        <button @click="showModal=false" class="modal-btn close-btn">Close</button>
      </div>


    </div>
    <div class="container">
      <header>  
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>

      <div class="cards-container">
        <div v-for="note in notes"
        :key="note.id"
        class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">
       {{ note.text}}

          </p>
          <p class="date">
          {{note.date.toLocaleDateString("ita-IT")}}
          </p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>

</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;

}

.container {
  max-width: 1100px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items:center;
}
textarea{
  padding:10px;
}

h1{
  font-weight:bold;
  margin-bottom:25px;
  font-size:75px;
  font-family: 'Lora', serif;
  font-family: 'Playfair Display', serif;
  font-family: 'Righteous', cursive;
  
}

button{
  border:none;
  padding:10px;
  width:50px;
  height:50px;
  cursor:pointer;
  background-color: rgba(236, 80, 18, 0.772);
  font-size:25px;
  border-radius: 100%;
  color:white;

}

.card{
  width:225px;
  height:225px;
  background-color:rgb(209, 209, 38);
  padding:10px;
  border-radius:15px;
  display: flex;
  flex-direction:column;
  justify-content:space-between;
  margin-right:20px;
  margin-bottom:20px;
  color:rgb(20, 21, 24);
}

.cards-container{
  display:flex;
  flex-wrap:wrap;
}

.date{
  font-size:12.5px;
  font-weight:bold;
}


.overlay{
  position:absolute;
  width:100%;
  height:100%;
  background-color:rgb(0,0,0, 0.77);
  z-index:10;
  display:flex;
  align-items:center;
  justify-content: center;
}

.modal{
  width:750px;
  background-color: white;
  border-radius:4px;
  padding:13px;
  position:relative;
  display:flex;
  flex-direction:column;
}

.modal-btn{
padding:10px 20px;
border-radius:4px;
font-size:20px;
width:100%;
background-color:#e5d62e;
color:white;
cursor:pointer;
margin-top:16px;

}

.modal p{

  color:red;
}
.close-btn{
  background-color: #d04918;
  margin-top:8px;
}
</style>