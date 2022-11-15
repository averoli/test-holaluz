<template>
  <h1>Get enrolled with the rooftop revolution.</h1>
  <SearchCups :clients="clients" />
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
