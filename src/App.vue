<template>
    <main class="container">
      <article>
        <h1 class="">Get enrolled with the rooftop revolution.</h1>
        <SearchCups :clients="clients" />
      </article>
    </main>
</template>

<script>
import SearchCups from "@/components/SearchCups";
import clients from "@/api/clients";
export default {
  data() {
    return { clients }
  },
  components: {
    SearchCups,
  },
};
</script>

<style>
</style>
