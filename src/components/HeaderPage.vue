<template>
  <header>
    <form @submit.prevent="$emit('queryChange', queryString)">
      <label for="query">
        <input
          id="query"
          v-model="queryString"
          type="text"
          name="query"
        >
      </label>
      <button>Cerca</button>
    </form>
  </header>
</template>

<script>
export default {
  name: 'HeaderPage',
  data() {
    return {
      queryString: '',
    };
  },
};
</script>

<style lang="scss" scoped>
  header {
    display: flex;
    justify-content: flex-end;
    padding: 1rem;
    background-color: salmon;
  }
</style>
