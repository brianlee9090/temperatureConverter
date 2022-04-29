<template>
  <div class="w-full" >
    <select id="unitList" v-model="selected" @change="handleChange"  class="h-11 w-full text-sm rounded" aria-labelledby="dropdownDefault">
      <option @click="handleClick" v-for="unit in units" :key="unit.name" :id="unit.name" :value="unit.value" >
        <a id="celsius" class="block px-4 py-2">{{unit.name}}</a>
      </option>
    </select>
  </div>
</template>

<script>

export default {
  data: function() {
    return {
      selected: "",
      units: [
  { name: 'Celsius ℃', value: "℉"},
  { name: 'Farenheit ℉', value: "℃" },
    ],};
  },
  methods: {
    handleChange(){
        this.$emit("unit-change", this.selected);
    },
    handleClick(){
        this.selected = this.unit.name
    }
  }
};
</script>