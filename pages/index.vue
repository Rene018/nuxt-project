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
            v-for="i in response"
            :key="i"
            :nombre="i.name"
            :url="i.id"
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
    };
  },
  mounted() {
    this.getInfo();
    for (let index = 0; index < 20; index++) {
        this.getImg(index)
    }

  },
  methods: {
    async getInfo() {
      const { data } = await this.$axios.get("pokemon");
      this.response = data.results;
    },
    async getImg(i) {
      const { data } = await this.$axios.get(`pokemon/${i}/`);
       this.response[i].push(data.id) 
    }
  },
};
</script>

<style></style>
