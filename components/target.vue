<template>
    <div class="flex flex-col bg-slate-200 p-3 rounded-xl" >
        <div ><img class="w-72" :src="url" alt=""></div>
        <h2 class="text-center font-bold text-3xl">{{ nombre }}</h2>
    </div>
</template>
    
<script>
    export default{
        name: 'target',
        data(){
            return{
            }
        },
        props:{
            nombre:{
                type: String,
                required: true
            },
            url:{
                type: String,
                required: true
            }
        }
    }
</script>
    
<style></style>