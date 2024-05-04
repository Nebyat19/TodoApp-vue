<template>
 

<div class="relative">
   <label :id="id" :class="{'bg-red-300': todo.done}" class="flex  hover:bg-slate-200 rounded-lg px-2 mt-3 items-center bg-gray-50   py-3  justify-between">
<label for="isDone"  class="flex  items-center gap-3">  
  <span :class="todo.catagory=='Personal' ? 'border-red-400'  :  'border-green-500'" class="w-4 h-4 p-1 bg-slate-200 rounded-full border-2"></span>
  <h1 class="text-md text-gray-800">{{ todo.content }}</h1>
<slot id="radio" name="makeDoneButton"></slot>

</label>

<div class="flex gap-2"><slot id="remove" name="removeTodo"></slot>

<button @click="isDialogOpen=!isDialogOpen" type="button" class="bg-gray-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Edit</button>
<div>
    

    <div v-if="isDialogOpen" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-white rounded w-[90%] px-5 py-5 max-w-md">
        <h2 class="text-2xl font-bold mb-4">Edit Todo</h2>
        <input :value="todo.content" class="w-full border outline-none focus:border-slate-500 text-gray-500 text-sm px-3 py-3 mt-1 rounded-md" type="text" placeholder="e.g make a video" />
      <div class="flex gap-5 mt-3">
        <button @click="saveTodo" type="button" class="bg-red-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Save</button>
      
      <button @click="isDialogOpen=!isDialogOpen" type="button" class="bg-gray-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Close</button>

      </div>
      </div>
    
    </div>
  </div>

</div>
</label>
  <hr v-if="todo.done" class="w-full absolute top-1/2  bg-gray-500">
 
</div>

    </template>


<script >

import { ref } from 'vue';
import DeleteButton from './DeleteButton.vue';
export default{
 props:['todo','id'],

  setup(props){
    const isDone =ref(false)
   const isDialogOpen = ref(false)
    return {isDone,isDialogOpen}
  }

}

</script>