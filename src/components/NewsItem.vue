<template>
  <article class="media">
    <figure class="media-left">
      <p class="image is-128x128">
        <img :src="image" alt="news-image" />
      </p>
    </figure>
    <div class="media-content">
      <div class="content">
        <strong>{{ news.title }}</strong>
        <br />
        <div>
          <div class="is-size-7 has-text-right">
            {{ new Date(news.pubDate).toLocaleDateString() }}
          </div>
          {{ news.description }}
          <br />
          <small class="is-size-7">@{{ news.dcCreator }}</small>
          <!-- {{ news.credit }} -->
        </div>
      </div>
    </div>
    <div class="media-right">
      <a
        :href="news.link"
        target="_blank"
        rel="noopener"
        class="button is-small is-rounded is-primary"
        >></a
      >
    </div>
  </article>
</template>

<script>
import img from "@/assets/no-image.jpg";
export default {
  props: ["news"],
  computed: {
    image() {
      return this.news.image || img;
    },
    date(dateStr) {
      return new Date(dateStr.toString()).toLocaleDateString();
    },
  },
};
</script>

<style scoped>
.button.is-rounded {
  padding-left: 0.85em;
  padding-right: 0.85em;
}
</style>
