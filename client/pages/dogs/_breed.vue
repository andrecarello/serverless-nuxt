<template>
  <div class="container py-10 mx-auto">
    <h1 class="text-2xl text-gray-800	text-center">Dog breed: {{ breed }}</h1>
    <div class="mt-20 grid grid-cols-3 gap-4">
      <img v-for="dog in dogs" v-bind:key="dog.id" :src="dog.url" class="h-64 w-full block object-cover" />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ store, $http, route }) {
    const dogs = await $http.$get("images/search?size=thumb&has_breeds=true&limit=50");

    const reg = new RegExp(route.params.breed, "g");
    const filteredDogs = dogs.filter(dog =>
      dog.breeds[0]
        .name
        .toLowerCase()
        .match(reg)
    );

    return { dogs: filteredDogs, breed: route.params.breed };
  },
  head() {
    return {
      title: `${this.breed} Dog`,
      meta: [
        {
          hid: "description",
          name: "description",
          content: `You are ${this.breed} hello 👋`
        }
      ]
    };
  }
};
</script>
