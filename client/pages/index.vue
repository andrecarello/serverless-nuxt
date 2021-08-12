<template>
  <div class="py-10">
    <h1 class="text-2xl text-gray-800	text-center">This is the Front Page.</h1>
    <h2 class="text-xl text-gray-800	text-center">Random dog of the day:</h2>
    <div class="container mx-auto">
      <div class="mt-20 grid grid-cols-1 gap-4">
        <img :src="dog.url" alt="" class="h-64 w-full block object-cover" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $http }) {
    const dogs = await $http.$get("https://api.thedogapi.com/v1/images/search?limit=1");
    return { dog: dogs[0] };
  }
};
</script>
