<template>
 

<div class="relative">
   <label :id="id" :class="{'bg-red-300': todo.done}" class="flex  hover:bg-slate-200 rounded-lg px-2 mt-3 items-center bg-gray-50   py-3  justify-between">
<label for="isDone"  class="flex  items-center gap-3">  
  <span :class="todo.catagory=='Personal' ? 'border-red-400'  :  'border-green-500'" class="w-4 h-4 p-1 bg-slate-200 rounded-full border-2"></span>
  <h1 class="text-md text-gray-800">{{ todo.content }}</h1>
<slot id="radio" name="makeDoneButton"></slot>

</label>

<div class="flex gap-2"><slot id="remove" name="removeTodo"></slot>

<button class="bg-gray-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Edit</button>
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
    return {isDone}
  }

}

</script>