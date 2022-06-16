<template>
  <div>
    <nav class="text-white bac block text-center">
      <RouterLink to="/">Home</RouterLink> |
      <RouterLink to="/products">Products</RouterLink>
    </nav>
    <RouterView />
  </div>
</template>

<script>
import { createClient, provideClient } from '@urql/vue';
export default {
  setup() {
    const client = createClient({
      url: 'http://38.242.229.113:8055/graphql',
    });
    provideClient(client)
  }
}
</script>

<style>
</style>