<template>
  <div class="bg-slate-100 w-full h-full flex justify-center">
    <form @submit.prevent="addTodo">
      <div
        class="flex pt-10 px-5 text-slate-900 w-full  flex-col gap-5 h-screen bg-slate-950"
      >
        <div class="flex  text-center items-center justify-start gap-3">
          <h2 class="text-lg flex font-bold whitespace-nowrap text-[#C0C0C0]">What's up,</h2>
          <input
            class="bg-slate-950 font-bold text-[#C0C0C0] outline-none inline-block"
            v-model="name"
            type="text"
            placeholder="Hetu"
          />
        </div>
        <div>
          <h2 class="uppercase text-lg text-[#C0C0C0]">Create a todo</h2>
          <h3 class="text-sm text-[#39FF14]">what's on your todo list?</h3>

          <IputField>
            <input
              v-model="input_content"
              class="w-full border outline-none focus:border-slate-500 text-gray-500 text-sm px-3 py-3 mt-1 rounded-md"
              type="text"
              placeholder="e.g make a video"
            />
          </IputField>
          <h1 class="text-sm text-[#39FF14] mt-5">Pick a ctagory</h1>

          <div  class="flex gap-5 align-middle mt-2">
            <label  for="catagory1" class="bg-white hover:bg-slate-200 rounded-md flex gap-3 p-5 grow">
            
               <input
                v-model="input_catagory"
                name="catagory"
                id="catagory1"
                value="Business"
                class="text-gray-950 checked:bg-red-500"
                type="radio"
               
              />
              <h1>Business</h1>
            </label>
            <label  for="catagory2" class="bg-white hover:bg-slate-200 rounded-md flex gap-3 p-5 grow">
              <input
                v-model="input_catagory"
                name="catagory"
                id="catagory2"
                value="Personal"
                class="text-gray-950 checked:bg-red-500"
                type="radio"
             
              />
              <h1>Personal</h1>
            </label> 
          </div>
          <button class="w-full " type="submit">  <AddButton/></button>
        
          <div class="text-center mt-3 uppercase text-red-500 text-xs">{{ errorMessage }}</div>
          <h1 class="text-sm text-[#39FF14] px-3 mt-5">Todo List</h1>
          <TodoItem @updateParentData="updateParentData" v-for="(todo,index) in todosComputed" :todos="todos" :todo="todo" :key="todo.input_content" :id="index" >
           <template #makeDoneButton>
    <input  class="hidden" v-model="todo.done" value="true" type="checkbox" id="isDone" name="isDone" > 
       
           </template>
            <template #removeTodo>
     <button  @click="removeTodo(todo)" type="button" class="bg-red-500 hover:bg-red-400 text-white py-1 px-2 rounded-md text-sm">Delete</button>

    </template> 
         </TodoItem>
          
        </div>
      </div>
    </form>
  </div>
 
</template>

<script setup>
import AddButton from '@/components/AddButton.vue'
import TodoItem from '@/components/TodoItem.vue'

import IputField from '@/components/IputField.vue'
import { computed, onMounted, ref, watch } from 'vue'


const todos = ref([])
const name = ref('')
const input_content = ref('')
const input_catagory = ref(null)
const errorMessage =ref('')
const todo=ref({})
const todosComputed = computed(() =>  todos.value.sort((a, b) =>{return b.createdAt - a.createdAt } )
)

const addTodo = () => {
  if(input_content.value.trim==='' || input_catagory.value==null)
{
  return errorMessage.value= "select catagory or input todo";
}
todo.value={
   id:todos.value.length+1,
   content:input_content.value,
   catagory:input_catagory.value, 
   createdAt:new Date().getTime() ,
   done: false
}
if(!isNew(todo)){
   
   todo.value=null
   return  errorMessage.value="Todo Already Exists"
}
todos.value.push(todo.value)

todo.value=null

}


const isNew=(todo)=>{
  return todos.value.every(t => t.content !== todo.value.content)
}
const removeTodo =(todo)=>{
  todos.value=todos.value.filter(t => t !==todo)

 }
watch(todos,newTodo=>{
   localStorage.setItem('todos',JSON.stringify(newTodo))
},{deep:true})
watch(name, (newValue) => {
  localStorage.setItem('name', newValue)
})

const updateParentData=(id, newData) =>{
  const index=todos.value.findIndex(t=>t.id===id)
  todos.value[index].content=newData

  console.log(todos.value)
    }
onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
  
 console.log(todos.value)

})
</script>
