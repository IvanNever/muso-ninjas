<template>
  <form @submit.prevent="handleSubmit">
    <h3>Sign up</h3>
    <input type="text" placeholder="Display name" v-model="displayName" />
    <input type="email" placeholder="Email" v-model="email" />
    <input type="password" placeholder="Password" v-model="password" />
    <div class="error" v-if="error">{{ error }}</div>
    <button v-if="isPending" disabled>Loading...</button>
    <button v-else>Sign up</button>
  </form>
</template>

<script>
import { ref } from "vue";

import useSignup from "@/composables/useSignup";

export default {
  setup() {
    const { error, signup, isPending } = useSignup();

    const displayName = ref("");
    const email = ref("");
    const password = ref("");

    const handleSubmit = async () => {
      await signup(email.value, password.value, displayName.value);

      if (!error.value) {
        console.log("user sign up");
      }
    };

    return { displayName, email, password, handleSubmit, error, isPending };
  },
};
</script>

<style></style>
