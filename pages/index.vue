<template>
  <div>
    <input v-model="email" type="email">
    <input v-model="password" type="password">
    <button @click="signInWithEmail()">Login</button>
  </div>
</template>

<script setup lang="ts">
const user = useSupabaseUser()
const { auth } = useSupabaseClient()
const email = ref('')
const password = ref('')

// Sign in with email
const signInWithEmail = async () => {
  const { error } = await auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  if (error) {
    return alert(error.message);
  }
  navigateTo("/auth");
};


// Check if user is logged in.
watchEffect(() => {
  if (user.value) {
    navigateTo("/auth");
  }
});
</script>