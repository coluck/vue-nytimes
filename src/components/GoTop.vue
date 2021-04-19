<template>
  <div ref="top" class="button is-primary top" @click="scrollTop">↑</div>
</template>

<script>
export default {
  mounted() {
    window.onscroll = () => {
      this.scrollFunction();
    };
  },
  methods: {
    scrollTop() {
      document.documentElement.scrollTop = 0;
    },
    scrollFunction() {
      if (
        document.body.scrollTop > 20 ||
        document.documentElement.scrollTop > 20
      ) {
        this.$refs.top.style.display = "block";
      } else {
        this.$refs.top.style.display = "none";
      }
    },
  },
};
</script>

<style scoped>
.top {
  display: none;
  position: fixed;
  bottom: 20px;
  right: 30px;
  z-index: 99;
}
</style>
