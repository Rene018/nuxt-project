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
          <input placeholder="buscar pokemon" class="h-11" type="text" />
        </div>
        <div class="flex flex-wrap gap-10">
          <target v-for="(item,index) in response" :key="index" :nombre="item.name" :imagen="item.name" />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      response: []
    };
  },

  methods: {
    async getInfo() {
      const { data } = await this.$axios.get("pokemon");
      this.response = data.results
      let cont=0
      console.log(data);
      for (const name of this.response) {
        const imagen = await this.getImg(name.name)
        // name.imagen = imagen
        this.response.imagen=imagen
        console.log(name);
        console.log(imagen)
        cont+=1
      }
      console.log(this.response);
    },
    async getImg(i) {
      const { data } = await this.$axios.get(`pokemon/${i}/`);
      return data.sprites.front_default

    }
  },
  async mounted() {
    await this.getInfo();

  }
};
</script>

<style></style>
