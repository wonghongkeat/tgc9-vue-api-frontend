<template>
    <div>
    
        <h1>Get all Faults</h1>
        <button v-on:click="loadFaults">Load faults</button>
        <div>
            <label>Filter faults by title:</label>
            <input type="text" v-model="searchTitle"/>
        </div>
        <div v-for="f in results" v-bind:key="f._id">
            <h2>{{f.title}}</h2>
            <ul>
                <li>Date: {{f.date}}</li>
                <li>Location: {{f.location}}</li>
                <li>Block: {{f.block}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created:async  function(){
        let response = await axios.get('https://3000-b7922321-9a58-4310-8255-84781f5cb1d2.ws-us03.gitpod.io/faults/');
        this.faults = response.data;
    },
    data:function(){
        return {
            'faults':[],
            'searchTitle':''
        }
    },
    methods:{
        loadFaults:async function(){
            let response = await axios.get('https://3000-b7922321-9a58-4310-8255-84781f5cb1d2.ws-us03.gitpod.io/faults/');
            this.faults = response.data;
        }
    },
    computed:{
        results:function(){
            return this.faults.filter((eachFault)=>{
                return eachFault.title.toLowerCase().includes(this.searchTitle.toLowerCase()); 
            })
        }
    }
}
</script>

<style scoped>

</style>