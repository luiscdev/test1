<template>
  <div class="grid grid-cols-4 p-10 gap-y-5">
    <div v-for="(post, index) in postsList" :key="index">
      <div class="border border-gray-300 rounded-lg w-[450px] p-5 space-y-3">
        <div class="flex space-x-3 items-center capitalize">
          <img src="/images/nophoto.png" alt="user-image" class="w-7" />
          <h1 class="font-semibold text-gray-700">
            {{ post.title }}
          </h1>
        </div>
        <div>
          <span class="text-sm px-2 py-0.5 rounded-full text-white" :class="post.completed ? 'bg-green-400' : ' bg-orange-400'">
            {{ post.completed ? "Completed" : "Not Completed" }}
          </span>
          <span>hellooooo</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

type Post = {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
};

let postsList = ref<Post[]>([]);

async function GetPosts() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    postsList.value = await response.json();
    console.log(response);
  } catch (error) {
    console.log(error);
  }
}

onMounted(() => {
  GetPosts();
});
</script>

<style scoped></style>
