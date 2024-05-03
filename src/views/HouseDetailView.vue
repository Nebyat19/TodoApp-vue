<template>
<div v-if="isError"><p>Loading home .....</p>
{{ err }}</div>
<div v-else>

<div class="bg-gray-100 p-5">
    <h1>id: {{ id }}</h1>
<h1>{{home.title}}</h1>
<p>{{home.description}}</p>
</div>
</div>
<component :is="isLoaded ? 'div' : 'p'">Loading...</component>
</template>

<script>
import axios from 'axios'
export default {
    props:['id'],
    data(){
        return{
            home:{},
            isLoaded:false,
            isError:false,
            err:''
        }
    },
    mounted(){
        try{
            axios.get(`http://localhost:3000/homes/${this.id}`)
        .then(res=>{this.home = res.data; this.isLoaded = true })
        .catch(err=>{console.log(err); this.isError = true ; this.err = err})
        
        }catch(err){
            console.log(err)
            this.isLoaded = false;
            this.isError = true ; this.err = err
        }
    
    }
    
}
</script>