<template>
  <div class="level is-mobile is-hidden-tablet sticky">
    <div class="level-left">
      <div class="level-item">
        <div class="dropdown is-hoverable">
          <div class="dropdown-trigger">
            <button
              class="button is-primary"
              aria-haspopup="true"
              aria-controls="dropdown-menu4"
            >
              {{ categories[active - 1].name }} ↓
            </button>
          </div>
          <div class="dropdown-menu" id="dropdown-menu4" role="menu">
            <div class="dropdown-content">
              <div class="dropdown-item">
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
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="level-right">
      <div class="level-item subtitle mr-4">
        <a href="https://github.com/coluck/vue-nytimes" class="has-text-white">
          vue-nytimes</a
        >
      </div>
    </div>
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
.level {
  background-color: #4dba87;
  z-index: 999;
}
.button.is-primary {
  background-color: #4dba87;
}
</style>
