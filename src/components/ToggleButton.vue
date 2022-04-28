<template>
    
<div class="flex items-center justify-end w-full">
  <label for="toggle" class="flex items-center cursor-pointer">
    <div class="relative">
      <input type="checkbox" id="toggle" class="sr-only" @change="handleToggle">
      <div class="block bg-gray-600 w-14 h-8 rounded-full"></div>
      <div class="dot absolute left-1 top-1 bg-white w-6 h-6 rounded-full transition"><p>☽</p></div>
    </div>
    
  </label>
</div>
</template>

<script>
export default {
  data: function() {
    return {
      toggleOn: false,
      };
  },
  methods: {
    handleToggle(){
        
        if (document.getElementById("toggle").checked === true){
          this.toggleOn = true
        } else {
          this.toggleOn = false
        }
        this.$emit("dark-toggle", this.toggleOn);
    },
  }
};
</script>

<style>
input:checked ~ .dot {
  transform: translateX(100%);
}
input:checked ~ .block {
  background: #1d4ed8;
}

</style>