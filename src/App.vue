<template>
  <main>
    <div class="overlay">
      <div class="modal">
        <textarea name="note" id="note" cols="30" rows="10"></textarea>
        <button>Add Note</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button>+</button>
      </header>
        <div class="cards-container">
          <div class="card">
            <p class="main-text">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sint laborum suscipit, dolor porro est quibusdam. Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sit omnis quo voluptate ratione alias deserunt dolorum quia, temporibus, porro, veritatis commodi atque? Nemo tempore expedita vero quis, eius adipisci at.</p>
            <p class="date"></p>
          </div>
          <div class="card">
            <p class="main-text">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sint laborum suscipit, dolor porro est quibusdam.</p>
            <p class="date"></p>
          </div>
        </div>
    </div>
  </main>
</template>

<script setup>
  import {ref} from "vue";
  const count = ref(0);
</script>

<style scoped>
  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .date{
    font-size: 12.5px;
    font-weight: bold;
  }
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100;
    color: white;
    font-size: 20px;
  }
  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }
  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
</style>