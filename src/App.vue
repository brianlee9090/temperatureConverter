<template>
  <div :class="isDark ? 'dark' : ''">
  <div id="background" class="dark:bg-slate-900">
    <div id="ui" class="md:w-3/5 mx-auto">
    <div class=" flex flex-col justify-center w-11/12 m-auto">
      <div class="flex flex-row justify-around w-11/12 items-center mx-auto mb-12" >
        <div class="w-3/5 justify-start">
        <p class="dark:text-slate-200 text-3xl font-extrabold  mx-auto text-left" id="title"> Temperature
        </p>
        </div>
        <div class="w-2/5 justify-end items-center">
        <ToggleButton @dark-toggle="this.isDark = ($event)" class="justify-end items-center	mx-auto"/>
        </div>
      </div>
      <div class="flex flex-row justify-center items-center sm:h-28 my-16 mx-0 w-full">
        
        <div class="shrink w-3/5 m-0">
          <div class="h-24 w-full m-0 flex-col justify-center items-center" v-show="(!this.showResult)">
            <div class="flex flex-row m-auto justify-center"><SearchIcon class="h-10 w-10 py-2 text-slate-500"/></div>
            <div><p class="dark:text-slate-200">Please enter a temperature input and unit</p></div>
          </div>
          <div class="h-24 w-full m-0 flex-col justify-center items-center" v-show="(this.showResult)">
            <label class="dark:text-slate-200 py-2">Result</label>
            <div class="flex flex-row justify-start m-0 h-16 w-full m-0">
            <p class="text-5xl text-right w-full dark:text-slate-200"  v-show="this.showResult">{{this.temperature}}</p>
            <p class="text-5xl text-center sm:text-left w-full dark:text-slate-200"  v-show="this.showResult">&nbsp;{{this.unit}}</p>
          </div>
          </div>
        </div>
      </div>
      <div class="flex flex-col justify-center w-full mt-10">
        <div class="flex flex-row justify-around items-center w-full m-0 mt-8 mb-2">
          <div class="flex flex-col justify-start flex-nowrap w-2/5 m-0" >
            <label class="dark:text-slate-200 text-left">Input here</label>
            <input class="h-11 w-5/5 rounded" @keyup.enter="onEnter" type="number" v-model="input" @input="handleInput">
          </div>
          <div class="flex flex-col justify-start flex-nowrap w-2/5 m-0 ">
            <label class="text-left dark:text-slate-200">Unit</label>
            <UnitList @unit-change="unit = $event" class="h-11 w-5/5"/>
          </div>
        </div>
        <div class="mt-4">
        <button id="convert" type="button" class="w-11/12 h-12 text-white bg-blue-700 hover:bg-blue-800 focus:ring-3 focus:ring-blue-300 font-medium rounded-lg text-sm dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" @click="handleConvert">Convert</button>
        </div>
      </div>
    </div>
    </div>
  </div>
  </div>
</template>

<script>
import ToggleButton from './components/ToggleButton.vue'
import UnitList from './components/UnitList.vue'
import { SearchIcon } from '@heroicons/vue/solid'


export default {
  name: 'App',
  components: {
    ToggleButton, UnitList, SearchIcon
  },
  
  data: ()=>({
    temperature: "--",
    unit: "",
    input:"",
    temperatureInput: "",
    showResult: false,
    isDark: false
  }),
  watch: {
    unit: "checkUnit"
    }
  ,
  methods: {
    handleInput(event){
     if (event.target.value.length > 5) {
        event.target.value = event.target.value.slice(0,5); 
     }
     if (event.target.value.length === 5) {
       this.onEnter()
    }
     this.temperatureInput = event.target.value.trim()
     this.showResult = false
    },
    handleConvert(){
      if (this.temperatureInput !== "" && this.unit === "℃"){
      this.temperature = ((this.temperatureInput - 32) * 5/9).toFixed(1)
      this.showResult = true;
      }
      if (this.temperatureInput !== "" &&  this.unit === "℉"){
      this.temperature = ((this.temperatureInput * 9/5)+32).toFixed(1)
      this.showResult = true;
      console.log(this.isDark, "isDark")
      }
    },
    checkUnit(){
        this.showResult = false
        if (this.temperatureInput !== "" & this.unit !== ""){
        this.handleNext()
      }
      },
    onEnter(){
      document.getElementById("unitList").focus();
    },
    handleNext(){
      document.getElementById("convert").focus()
    }
    }
  }
</script>

<style>
#background{
  height: 100vh;
  width: 100vw;
  margin:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  justify-items: center;
  align-items: center;
  margin: auto;
  height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 0;
}
#ui{
  padding-top: 8vh;
}
</style>
