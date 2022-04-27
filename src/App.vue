<template>
  <div :class="isDark ? 'dark' : ''">
  <div id="background" class="dark:bg-slate-900">
    <div id="ui" class="md:w-3/5 mx-auto">
    <div class=" flex flex-col justify-center w-11/12 m-auto">
      <div class="flex flex-row justify-around w-11/12 items-center mx-auto" >
        <div class="w-3/5 justify-start">
        <p class="dark:text-slate-200 text-3xl font-extrabold  mx-auto text-left" id="title"> Temperature
        </p>
        </div>
        <div class="w-2/5 justify-end items-center">
        <ToggleButton @dark-toggle="this.isDark = ($event)" class="justify-end items-center	mx-auto"/>
        </div>
      </div>
      <div class="flex flex-row justify-center items-center	my-16 mx-0 w-full">
        <div class="shrink w-3/5 m-0">
          <label class="dark:text-slate-200">Result</label>
          <div class="h-16 w-full m-0" v-show="(!this.showResult)"></div>
          <div class="flex flex-row justify-start m-0 h-16 w-full m-0" v-show="(this.showResult)">
          <p class="text-5xl w-full dark:text-slate-200"  v-show="this.showResult">{{this.temperature}}</p>
          <p class="text-5xl w-full dark:text-slate-200"  v-show="this.showResult">{{this.unit}}</p>
          </div>
        </div>
      </div>
      <div class="flex flex-col justify-center w-full m-0">
        <div class="flex flex-row justify-around items-center w-full m-0">
          <div class="flex flex-col justify-start flex-nowrap w-2/5 m-0" >
            <label class="dark:text-slate-200 text-left">Input here</label>
            <input class="w-5/5 border-b-2" @keyup.enter="onEnter" type="tel" maxlength="4" v-model="input" @input="handleInput">
          </div>
          <div class="flex flex-col justify-start flex-nowrap w-2/5 m-0 ">
            <label class="text-left dark:text-slate-200">Unit</label>
            <UnitList @unit-change="unit = $event" class="w-5/5"/>
          </div>
        </div>
        <div>
        <button id="convert" type="button" class="mt-3 w-11/12 h-8 text-white bg-blue-700 hover:bg-blue-800 focus:ring-3 focus:ring-blue-300 font-medium rounded-lg text-sm dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" @click="handleConvert">Convert</button>
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

export default {
  name: 'App',
  components: {
    ToggleButton, UnitList
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
      this.temperatureInput = event.target.value.trim()
      console.log(this.temperatureInput)
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
      document.getElementById("unitList").click();
    },
    handleNext(){
      document.getElementById("convert").focus()
      this.handleConvert()
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
