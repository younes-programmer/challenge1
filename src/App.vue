<template>
     <nav>
        <div class="logo">
            <img src="./assets/logo.png" alt="logo">
        </div>
        <h3>School Name</h3>
    </nav>
        <div class="sidebar">
        <div class="sidebar-title"><i class="fas fa-clock"></i> Waiting List</div>
        <div class="box" v-for="info in infosParents" :key="info.cin">
          <div class="users">
              <!-- <i class="fas fa-user"></i> -->
              <h4>{{ info.name }}</h4>
          </div>
        </div>
    </div>

    <div class="container">
        <div class="main-box parent">
          <!-- :src="this.infosParent[this.i].url" -->
            <img  src="./assets/parent2.png" alt="image-parent" id="parent-image">
            <h2 class="heading-name" id="parent-name" ref="parentname">John Doe</h2>
            <h3 class="heading-work" id="parent-city">Address</h3>
        </div>
        <div class="main-box student">
            <img src="./assets/child2.png" alt="image-student" id="child-image">
            <h2 class="heading-name" id="child-name">John doe</h2>
            <h3 class="heading-work" id="child-city">Address</h3>
        </div>
    </div>
    <div class="valider">
      <!-- <button @click="handleData" id="btn">Valider</button> -->
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
// import VueAxios from 'vue-axios'
export default {
  name: 'App',
  data(){
      return{
      infosParents: [],
      infosChildren: [],
      i: 0
    }
  },
  mounted(){
    setInterval(() => {
      this.handleData()
    }, 2000)
  }
  ,
  async created(){
    try{
      const res = await axios.get("http://localhost:3000/parents");
      const secondeRes = await axios.get("http://localhost:3000/students")
      this.infosParents = res.data;
      this.infosChildren = secondeRes.data
    }catch(err){
      console.log(err);
    }
  },
  methods: {
    handleData(){
      const btn = document.getElementById("btn");
      const parentImage = document.getElementById("parent-image")
      const parentName = document.getElementById("parent-name")
      const parentCity = document.getElementById("parent-city")
      const childImage = document.getElementById("child-image")
      const childName = document.getElementById("child-name")
      const childCity = document.getElementById("child-city")
      if(this.i === this.infosParents.length){
        // btn.style.background = "crimson"
        // btn.style.cursor = "not-allowed"
        this.i = 0
        return
      }
      parentImage.src = require(`${this.infosParents[this.i].url}`)
      parentName.innerHTML = `${this.infosParents[this.i].name}`
      parentCity.innerHTML = `${this.infosParents[this.i].city}`
      childImage.src = require(`${this.infosChildren[this.i].url}`)
      childName.innerHTML = `${this.infosChildren[this.i].name}`
      childCity.innerHTML = `${this.infosChildren[this.i].city}`
      this.infosParents[this.i].waitingState = false
      this.i = this.i + 1
  }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.valider{
  position: absolute;
  bottom: 0px;
  left: 50%;
  margin: 20px auto;
  text-align: center;
}
.valider button{
  width: 150px;
  height: 40px;
  border-radius: 20px;
  border: 1px solid transparent;
  background: #108a51;
  color: white;
  font-weight: 600;
  font-size: 16px;
  cursor: pointer;
}
.valider button:hover{
  background: #3c996d;
}
nav {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 70px;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #EEE;
    border-bottom: 3px solid rgba(192, 192, 192,1);
}
nav .logo img {
    width: 50px;
    height: 40px;
}
nav h3 {
    font-family: 'Dancing Script', cursive;
    font-size: 27px;
    font-weight: 600;
    color: #b42dfd;
}
.sidebar {
  position: absolute;
  width: 18%;
  height: 720px;
  top: 73px;
  left: 0;
  background-color: white;
  overflow-y: scroll;
}
.sidebar .sidebar-title {
  width: 100%;
  min-height: 10%;
  color: #46e097;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 22px;
  margin-top: 20px;
  /* border-bottom: 1px solid #146ebe; */
}
.sidebar .users {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  padding: 0px 10px;
  margin: 10px 0;
}
.sidebar .users i {
  margin-right: 10px;
}
.container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-40%,-50%);
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 100px;
}
.container .main-box:last-child {
    box-shadow: 2px 4px 2px 4px rgba(187, 98, 235, 0.8);
}
.main-box {
    width: 300px;
    height: 300px;
    box-shadow: 2px 4px 2px 4px rgba(70, 224, 151, 0.65);
    border-radius: 10px;
    text-align: center;
    padding: 20px 0;
}
.container .main-box:last-child .heading-work {
    color: #A600FF;
    font-weight: 500;
}
.container .main-box img{
  height: 200px;
  width: 200px;
  object-fit: cover;
  border-radius: 50%;
  border: 5px solid rgba(70, 224, 151, 0.65);
}
.container .main-box:last-child img{
  border: 5px solid rgba(187, 98, 235, 0.8);
}

.heading-name {
 margin: 10px 0;   
}

.heading-work {
    color: #46E097;
    font-weight: 500;
    margin: 3px 0;
}
p {
    padding: 0 20px;
    margin-bottom: 25px;
}

.follow_btn {
    text-decoration: none;
    background: #46E097;
    color: #fff;
    padding: 10px 20px;
    border-radius: 20px;
    box-shadow: 2px 2px 1px 1px rgba(70, 224, 151, 0.65);
}

.follow_btn:hover{
    color: #46E097;
    background: #DAF9F6;
    font-weight: 600;
}
</style>
