<template>
  <div v-if="loading">Loading...</div>
  <div v-else class="flex justify-center items-center mt-52">
    <div class="w-full max-w-xl">
      <h1 class="uppercase text-3xl text-red-500">{{ error }}</h1>
      <form
        class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4"
        @submit="handlesubmit"
      >
        <div class="identity-input mb-4">
          <label
            for="identity"
            class="block text-gray-700 text-sm font-bold mb-2"
          >
            Email</label
          >
          <input
            id="identity"
            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            type="text"
            placeholder="Email"
            aria-describedby="emailHelp"
            v-model="email"
          />
          <span class="text-xs text-red-700" id="emailHelp"></span>
        </div>

        <div class="password-input mb-6">
          <label
            for="identity"
            class="block text-gray-700 text-sm font-bold mb-2"
            >Password</label
          >
          <input
            aria-describedby="passwordHelp"
            class="shadow appearance-none borderrounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            id="password"
            type="password"
            placeholder="*******"
            v-model="password"
          />
          <span class="text-xs text-red-700" id="passwordHelp"></span>
        </div>
        <div class="flex items-center justify-between">
          <button
            class="bg-blue-600 hover:bg-black text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            type="submit"
          >
            Register
          </button>
          <div class="text-xl font-semibold">
            Have Account
            <NuxtLink to="/login" class="text-blue-700">Login </NuxtLink>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
definePageMeta({
  layout: false,
});
export default {
  data() {
    return {
      email: "",
      password: "",
      loading: false,
      error: "",
    };
  },
  methods: {
    handlesubmit(e) {
      e.preventDefault();
      this.loading = true;
      const email = this.email;
      const password = this.password;
      axios
        .post("https://my-basecamp-eta.vercel.app/api/v1/register", {
          email: email,
          password: password,
        })
        .then((res) => {
          this.error = "";
          localStorage.setItem("id", res.data.user._id);
          navigateTo("/");
        })
        .catch((err) => {
          this.error = err.response.data.error;
          console.log(err);
        });
      this.loading = false;
    },
  },
  mounted() {
    if (localStorage.getItem("id")) {
      navigateTo("/");
    }
  },
};
</script>
