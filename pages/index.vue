<template>
  <div class="pt-[3%]">
    <div v-for="item in data" :key="item._id" class="flex items-center justify-center text-center">
      <div class="w-full max-w-xl bg-blue-300 my-5">
        <div class="text-3xl text-blue-700">{{item.name}}</div>
        <div class="text-xl text-red-700">{{item.description}}</div>
        <div v-if="item.user_id == id">
          <NuxtLink :to="`/edit/${item._id}`">
            Edit
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
if (process.client) {
  const id = localStorage.getItem("id");
  if (!id) {
    navigateTo("/login");
  }
}
</script>
<script>
import axios from 'axios';

export default {
  data () {
    return {
      data: [],
      id: ''
    }
  },
  mounted() {
    this.id = localStorage.getItem("id");
    axios.get('http://localhost:8888/api/v1/project')
      .then(res => {
        this.data = res.data.project;
      })
      .catch(err => {
        console.error(err);
      });
  },
};
</script>