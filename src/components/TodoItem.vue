<template>
 

<div class="relative">
   <label :id="id" :class="{'bg-red-300': todo.done}" class="flex  hover:bg-slate-200 rounded-lg px-2 mt-3 items-center bg-gray-50   py-3  justify-between">
<label for="isDone"  class="flex  items-center gap-3">  
  <span :class="todo.catagory=='Personal' ? 'border-red-400'  :  'border-green-500'" class="w-4 h-4 p-1 bg-slate-200 rounded-full border-2"></span>
  <h1 class="text-md text-gray-800">{{ todo.content }}</h1>
<slot id="radio" name="makeDoneButton"></slot>

</label>

<div class="flex gap-2"><slot id="remove" name="removeTodo"></slot>

<button @click="isDialogOpen=!isDialogOpen" type="button" class="bg-[#39FF14] hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Edit</button>
<div>
    

    <div v-if="isDialogOpen" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-white rounded w-[90%] px-5 py-5 max-w-md">
        <h2 class="text-2xl font-bold mb-4">Edit Todo</h2>
        <input  v-model="newContent" class="w-full border outline-none focus:border-slate-500 text-gray-500 text-sm px-3 py-3 mt-1 rounded-md" type="text" placeholder="e.g make a video" />
      <div class="flex gap-5 mt-3">
        <button @click="updateParent(todo,newContent)" type="button" class="bg-red-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Save</button>
      
      <button @click="isDialogOpen=!isDialogOpen" type="button" class="bg-gray-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Close</button>

      </div>
      <div class="text-xs text-center text-red-500" v-if="errorMessage">{{ errorMessage }}</div>
      </div>
    
    </div>
  </div>

</div>
</label>
 
 
</div>

    </template>


<script >

import { ref } from 'vue';

export default{
 props:['todo','id'],

  setup(){
    const isDone =ref(false)
    const isDialogOpen = ref(false)
    const newContent = ref('')
  
    
    return {isDone,isDialogOpen,newContent}
  },
 data(){
  return {
     errorMessage:''

  }
 },
  methods:{
    updateParent(todo,newContent){
     
      if(newContent==='') return this.errorMessage="content Can not be empty!"
      this.isDialogOpen=!this.isDialogOpen
      this.$emit('updateParentData',todo.id,newContent)
    }
  
  }
}

</script>