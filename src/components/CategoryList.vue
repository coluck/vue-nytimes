<template>
  <div class="menu sticky">
    <h1 class="subtitle has-text-centered">Categories</h1>
    <ul class="menu-list">
      <CategoryItem
        v-for="category in categories"
        :category="category"
        :key="category.id"
        :active="active === category.id ? true : false"
        @changeCategory="changeCategory"
      />
    </ul>
  </div>
</template>

<script>
import CategoryItem from "@/components/CategoryItem";
export default {
  props: ["categories", "active"],
  components: {
    CategoryItem,
  },
  methods: {
    changeCategory(category) {
      this.$emit("changeCategory", category);
    },
  },
};
</script>
<style scoped>
.menu.sticky {
  top: 1.25rem;
}
</style>
