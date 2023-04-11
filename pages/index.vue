<template>
    <div>
        <header class="flex justify-center m-4">
            <div class="flex justify-center items-center h-[10vh] w-[90vw] rounded-lg bg-gray-200">
                <h1 class="text-6xl font-medium">Poke Dex</h1>
            </div>

        </header>
        <main class="flex justify-center">
            <div class="flex w-[98vw] flex-col">
                <div class="flex">
                    <input placeholder="buscar pokemon" class="h-11" type="text">
                </div>
                <div class="flex flex-wrap gap-10 ">
                    <target v-for="i in response" :key="i" :nombre="i.name" :url="i.front_default"/>
                </div>
            </div>
        </main>
    </div>
</template>
    
<script>
export default {

    name: 'IndexPage',
    data() {
        return {
            response: [],
            imgg: []
        }
    },
    mounted() {
        this.getInfo()
        this.getImg()
    },
    methods: {
        async getInfo(){
            const {data} = await this.$axios.get('pokemon')
            this.response= data.results

        },
        async getImg(){
            for (let index = 0; index < this.response.length; index++) {
            const {img} = await this.$axios.get(`pokemon/${this.response.name}`)
            this.imgg= img.sprite
                
            }

        },


    }

}
</script>
    
<style></style>