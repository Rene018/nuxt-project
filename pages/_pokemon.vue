<template>
    <div>
        <loading v-if="loading" />
    <div v-else class="flex w-screen h-screen flex-col bg-indigo-200">
        <div class="m-10">
            <h1 class="text-center font-semibold text-5xl">{{ name }} </h1>
        </div>
        <div class="flex justify-center items-center gap-[20%]">
            <div><img class="w-72" :src="imagen"></div>
            <div class="flex border">
                <div>
                    <h1>Stats</h1>
                    <h2 v-for="(item, index) in estadisticas" :key="index">{{ item.stat.name }}: {{ item.base_stat }}</h2>
                </div>
                <div>
                    <h1>Abilities</h1>
                    <ul>
                        <li v-for="(item, index) in habilidades" :key="index">{{ item.ability.name }}</li>
                    </ul>

                </div>
            </div>
        </div>
    </div>
    </div>

</template>
    
<script>
import Loading from '~/components/loading.vue';

export default {
    name: "PokemonPage",
    data() {
        return {
            name: "",
            imagen: "",
            habilidades: [],
            estadisticas: [],
            imagenes: [],
            loading: true
        };
    },
    mounted() {
        this.getInfo();
        // this.busqueda()
    },
    methods: {
        async getInfo() {
            try {
                const { data } = await this.$axios.get(`pokemon${this.$route.fullPath}`);
                this.name = data.name;
                this.imagen = data.sprites.other.home.front_default;
                this.imagenes = data.sprites;
                this.habilidades = data.abilities;
                this.estadisticas = data.stats;
                this.loading=false
                console.log(data);
            }
            catch (error) {
                console.log(error);
            }
        },
        // async busqueda() {
        //     this.$router.push('/')
        // }
    },

}
</script>
    
<style></style>