<script setup>
import { ref } from 'vue'

const msg = ref('Hello World!')
const events = ref(
  [
  {id: 1, title: "Bookworm festival", desc: "Lorem ipsum", date: "30.11.25 11:30", i: "https://media.newyorker.com/photos/59ee325f1685003c9c28c4ad/master/w_2240,c_limit/Heller-Kirkus-Reviews.jpg$0"},
  {id: 2, title: "History of the Tea", desc: "Lorem ipsum", date: "30.11.25 12:30", i: "https://plus.unsplash.com/premium_photo-1674406481284-43eba097a291?q=80&w=2370&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D$0"},
  {id: 3, title: "Planes physics", desc: "Lorem ipsum", date: "11.12.25 16:20", i: "https://images.unsplash.com/photo-1483375801503-374c5f660610?q=80&w=2370&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D$0"},
  {id: 4, title: "Films secrets", desc: "Lorem ipsum", date: "22.12.25 18:00", i: "https://images.unsplash.com/photo-1485846234645-a62644f84728?q=80&w=2659&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D$0"},
  {id: 4, title: "Programming tips", desc: "Lorem ipsum", date: "28.12.25 10:00", i: "https://images.unsplash.com/photo-1498050108023-c5249f4df085?q=80&w=2372&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D$0"},
  ]
)

const showInfo = ref(false)
// <Tab :title="msg" description="Libre dolor"></Tab>
const registered = ref([]);

var url = "https://barcodeapi.org/api/qr/"

function register(id){
  if (registered.value.indexOf(id) === -1) {
    registered.value.push(id)
  }else {
    return;
  }
}

function findById(id) {
  return events.value.indexOf(id)

}

</script>

<template>
  <div>
    <div class="upper">
        <h2>Events</h2>
        <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#1f1f1f" @click="showInfo = true"><path d="M200-80q-33 0-56.5-23.5T120-160v-480q0-33 23.5-56.5T200-720h80q0-83 58.5-141.5T480-920q83 0 141.5 58.5T680-720h80q33 0 56.5 23.5T840-640v480q0 33-23.5 56.5T760-80H200Zm0-80h560v-480H200v480Zm280-240q83 0 141.5-58.5T680-600h-80q0 50-35 85t-85 35q-50 0-85-35t-35-85h-80q0 83 58.5 141.5T480-400ZM360-720h240q0-50-35-85t-85-35q-50 0-85 35t-35 85ZM200-160v-480 480Z"/></svg>
        
    
    </div>
    <p class="badge" v-if="registered.length">{{registered.length}}</p>
  </div>
  <div class="gr">

    <div class="card"  v-for="event in events" :key="event.id">

      <img :src="event.i"/>

      <h4>{{event.title}}</h4>

      <p>{{event.desc}}</p>

      <button type="button" @click="register(event.id)">Register <br>{{event.date}}</br></button>
    </div>

  </div>


  <div class="tickets" v-if="showInfo" @click="showInfo = false">
    <div class="overflow">
    <div class="window" v-for="ticket in registered">
      <h3>{{events[ticket-1].title}}</h3>
      <p>{{events[ticket-1].date}}</p>
      <div style='text-align: center;'>
      <img :src="url + ' ' + events[ticket-1].id +  events[ticket-1].date" />
    </div>  
    </div>
  </div>

  </div>
</template>

<style>

  body {
    margin: 0px;
  }

  .tickets {
    position:fixed;
    top: 0px;
    width: 100%;
    height: 100%;
    overflow: scroll;
    background-color: rgba(0,0,0,0.7);
    padding-top: 20px;
  }

  .window {
    padding: 10px;
    width: 60%;
    background-color: white;
    text-align: center;
    margin: auto;

  }

  .upper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-left: 20px;
    padding-right: 20px;
    z-index: 1;
  }

  .badge {
    color: white;
    position: absolute;
    top: -6px;
    height: 20px;
    z-index: 0;
    width: 20px;
    right: 10px;
    text-align: center;
    border-radius: 100px;
    
    background-color: #90A955;
  }

  .gr {
    display: grid;
    grid-template-columns: 1fr 1fr;
    
  }

  .card {
    border:2px solid #90A955;
    border-radius: 10px;
    padding: 15px;
    margin:10px;
  }

  button {
    background-color: #90A955;
    color: aliceblue;
    height: 50px;

    width: 100%;
    border-radius: 10px;
  }

  img {
    width: 100%;
    border-radius: 10px;
  }



  @media (max-width: 430px) {
    .gr {
      display: block;
    }
  }
</style>
