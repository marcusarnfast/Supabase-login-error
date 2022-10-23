<template>
  <div>
    <h1>Secure page</h1>
    <button @click="signOut()"> Log out</button>
    <button @click="client.auth.signOut()"> Log out</button>
  </div>
</template>

<script setup lang="ts">
const client = useSupabaseClient()

const router = useRouter()

definePageMeta({
  middleware: "auth",
});

//Sign out
const signOut = async () => {
  const { error } = await client.auth.signOut()
  if (error) {
    console.log(error)
  }
  return router.push("/")
}

</script>