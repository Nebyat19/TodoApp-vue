<template>
  <div  class="bg-white hover:bg-slate-200 rounded-md  flex gap-3 p-5 grow">
    <input :class="Class" class="text-gray-950 checked:bg-red-500" type="radio" name="" id="">
    <h1> </h1>
  
  </div>

    </template>

   
<script>
export default{
   props:["Class"],
    setup(){

    }

}
</script>