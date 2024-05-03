<template>
    <div v-if="!houses.length">loading .....</div>
<div class="class mt-10 py-5 px-3 bg-gray-50" :key=" index" v-for="(home, index) in houses">
<h1 class="uppercase mb-1 text-gray-800">{{home.title}}</h1>
<p class="text-sm font-semibold text-gray-500 mb-3">{{home.description}}</p>
<RouterLink :to="{ name: 'HouseDetail', params:{id:index}}"><button class="px-3 py-1 text-sm border border-gray-500 rounded lg uppercase mt-3">Detail</button></RouterLink>
</div>
<span v-if="err">  {{ err }}</span>
</template>

<script >



export default{
  props:['err','houses'],
  
}
</script>
