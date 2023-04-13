<template>
    <nuxt-link :to="nombre">
        <div class="flex flex-col bg-slate-200 p-3 rounded-xl">
            <div><img class="w-56" :src="imagen" alt=""></div>
            <h2 class="text-center font-bold text-3xl">{{ nombre }}</h2>
        </div>
    </nuxt-link>
</template>
    
<script>
export default {
    name: 'target',
    data() {
        return {
        }
    },
    props: {
        nombre: {
            type: String,
            required: true
        },
        imagen: {
            type: String,
            required: true
        }

    }
}
</script>
    
<style></style>