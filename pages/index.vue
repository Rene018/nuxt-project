<template>
  <div>
    <header class="flex justify-center m-4">
      <div
        class="flex justify-center items-center h-[10vh] w-[90vw] rounded-lg bg-gray-200"
      >
        <h1 class="text-6xl font-medium">Poke Dex</h1>
      </div>
    </header>
    <main class="flex justify-center">
      <div class="flex w-[98vw] flex-col">
        <div class="flex">
          <input placeholder="buscar pokemon" class="h-11" type="text" />
        </div>
        <div class="flex flex-wrap gap-10">
          <target
            v-for="(item, index) in response"
            :key="index"
            :nombre="item.name"
            :imagen="item.imagen"
          />
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
      response: [],
      imagenes: [],
    };
  },
  methods: {
    async getInfo() {
      const { data } = await this.$axios.get("pokemon");
      this.response = data.results;

      console.log(data);
      for (let index = 0; index < this.response.length; index++) {
        const element = this.response[index];
        const imagen = await this.getImg(element.name);
        this.imagenes.push(imagen);
        this.response[index].imagen = this.imagenes[index];
      }
      for (let index = 0; index < this.response.length; index++) {
        this.response[index].imagen = this.imagenes[index];
      }
      // for (const name of this.response) {
      //   const imagen = await this.getImg(name.name)
      //   // name.imagen = imagen
      //   this.response.imagen=imagen
      //   console.log(name);
      //   console.log(imagen)
      // }
    },
    async getImg(i) {
      const { data } = await this.$axios.get(`pokemon/${i}/`);
      return data.sprites.front_default;
    },
  },
  async mounted() {
    await this.getInfo();
    console.log(this.response);
  },
};
</script>

<style></style>
