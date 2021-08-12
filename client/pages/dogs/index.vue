<template>
  <div class="container py-10 mx-auto">
    <h1 class="text-2xl text-gray-800	text-center">Here you have all dogs.</h1>
    <div class="mt-20 grid grid-cols-3 gap-4">
      <img v-for="dog in dogs" v-bind:key="dog.id" :src="dog.url" class="h-64 w-full block object-cover" />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $http }) {
    const dogs = await $http.$get("images/search?size=thumb&limit=10");
    return { dogs };
  },
  head() {
    return {
      title: "Show all dogs!",
      meta: [
        {
          hid: "description",
          name: "description",
          content: `Hello Dogs 👋`
        }
      ]
    };
  }
};
</script>
