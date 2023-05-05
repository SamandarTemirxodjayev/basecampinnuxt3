<template>
  <!-- <div v-if="loading">Loading...</div> -->
  <div class="flex justify-center items-center mt-52">
    <div class="w-full max-w-xl">
      <h1 class="text-3xl text-blue-500 font-semibold">Edit Project!!!</h1>
      <form
        class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4"
        @submit="handlesubmit"
      >
        <div class="identity-input mb-4">
          <label
            for="identity"
            class="block text-gray-700 text-sm font-bold mb-2"
          >
            Name</label
          >
          <input
            id="identity"
            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            type="text"
            placeholder="Name"
            aria-describedby="emailHelp"
            required
            v-model="project.name"
          />
          <span class="text-xs text-red-700" id="emailHelp"></span>
        </div>

        <div class="password-input mb-6">
          <label
            for="identity"
            class="block text-gray-700 text-sm font-bold mb-2"
            >Description</label
          >

          <input
            aria-describedby="passwordHelp"
            required
            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            id="password"
            type="text"
            placeholder="Description"
            v-model="project.description"
          />

          <span class="text-xs text-red-700" id="passwordHelp"></span>
        </div>

        <div class="flex items-center justify-between">
          <button
            class="bg-blue-600 hover:bg-black text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            type="submit"
          >
            Create
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";


const fetchData = async () => {
  const route = useRoute();
  const id = route.params.id;
  const response = await axios.get(`http://localhost:8888/api/v1/project/${id}`);
  return response.data;
};

const project = ref([]);

onMounted(async () => {
  project.value = await fetchData();
});
function handlesubmit(e) {
  
  const route = useRoute();
  const id = route.params.id;
  e.preventDefault();
  const data = {
    name: project.value.name,
    description: project.value.description,
  };
  axios
  .post(`http://localhost:8888/api/v1/project/${id}`, data)
  .then((res) => {
      window.location.href = `/`;
    })
  .catch((err) => {
      console.log(err);
    });
}
</script>
