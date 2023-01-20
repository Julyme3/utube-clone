<template>
  <input
    type="text"
    placeholder="Search"
    class="w-full px-3 shadow-inner rounded-bl-sm rounded-tl-sm border border-gray-300 focus:border-blue-700 focus:outline-none"
  />
</template>

<script>
export default {
  name: 'TheSearchInput',
  mounted() {
    if (window.innerWidth < 640) {
      this.$el.focus();
    }
  },
};
</script>

<style scoped></style>
