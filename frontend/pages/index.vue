<template>
  <div class="container">
    <h1>Список Фрэймворков</h1>
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      <li v-for="framework in frameworks" :key="framework.id">
        {{ framework.name }}
        <br>
        <small>
          {{ framework.description }}
        </small>
      </li>
    </ul>
  </div>
</template>

<script>
  import axios from "../.nuxt/axios";

  export default {
    name: 'App',
    data () {
      return {
        frameworks: [],
        error: null
      }
    },
    async mounted () {
      try {
        this.frameworks = await this.$axios.$get('http://localhost:1337/frameworks')
      } catch (error) {
        this.error = error
      }
    }
  }
</script>

<style>
  ul {
    padding: 0;
  }
  li {
    list-style: none;
    margin-bottom: 10px;
    border-bottom: 1px solid gray;
  }
  h1 {
    margin-bottom: 1rem;
  }
  .container {
    padding: 1rem;
  }
</style>
