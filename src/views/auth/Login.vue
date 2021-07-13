<template>
  <form @submit.prevent="handleSubmit">
    <h3>Login</h3>
    <input type="email" placeholder="Email" v-model="email" />
    <input type="password" placeholder="Password" v-model="password" />
    <div class="error" v-if="error">{{ error }}</div>
    <button v-if="isPending" disabled>Loading...</button>
    <button v-else>Log in</button>
  </form>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";

import useLogin from "@/composables/useLogin";

export default {
  setup() {
    const { error, login, isPending } = useLogin();

    const router = useRouter();

    const email = ref("");
    const password = ref("");

    const handleSubmit = async () => {
      await login(email.value, password.value);

      if (!error.value) {
        router.push({ name: "UserPlaylists" });
      }
    };

    return { email, password, handleSubmit, error, isPending };
  },
};
</script>

<style></style>
