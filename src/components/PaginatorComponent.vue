<template>
  <div class="paginator">
    <button
      :disabled="(page === 1)"
      @click="$emit('changePage', page - 1)"
    >
      &lt;&lt;
    </button>
    Page: {{ page }} of {{ maxPages }}
    <button
      :disabled="(page === maxPages)"
      @click="$emit('changePage', page + 1)"
    >
      &gt;&gt;
    </button>
  </div>
</template>

<script>
export default {
  name: 'PaginatorComponent',
  props: {
    page: Number,
    maxPages: Number,
  },
};
</script>

<style lang="scss" scoped>
.paginator {
  text-align: center;
}
</style>
