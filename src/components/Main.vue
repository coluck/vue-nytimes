<template>
  <div class="container">
    <CategoryListMobile
      :categories="categories"
      :active="activeCategory"
      @changeCategory="changeCategory"
    />
    <div class="columns mt-2">
      <div class="column is-3 is-hidden-mobile is-fullheight">
        <CategoryList
          :categories="categories"
          :active="activeCategory"
          @changeCategory="changeCategory"
        />
      </div>
      <div class="column is-6">
        <h1 class="subtitle has-text-centered">News</h1>
        <div class="notification is-danger" v-if="errorMessage">
          {{ errorMessage }}
        </div>
        <NewsItem v-for="news in newsList" :news="news" :key="news.title" />
      </div>
      <div class="column is-3">
        <RightPanel />
      </div>
    </div>
    <GoTop />
  </div>
</template>

<script>
import { getFirst, getAttr, getAllItem } from "@/utils.js";
import categoryData from "@/categoryData";

import NewsItem from "@/components/NewsItem";
import CategoryList from "@/components/CategoryList";
import CategoryListMobile from "@/components/CategoryListMobile";
import RightPanel from "@/components/RightPanel";
import GoTop from "@/components/GoTop";

export default {
  components: {
    NewsItem,
    CategoryList,
    CategoryListMobile,
    RightPanel,
    GoTop,
  },
  data() {
    return {
      categories: categoryData,
      activeCategory: 1,
      xmlUrl: "https://rss.nytimes.com/services/xml/rss/nyt/HomePage.xml",
      hideMobile: true,
      newsList: [],
      xmlDoc: null,
      errorMessage: "",
    };
  },
  created() {
    this.fetchXml(this.xmlUrl);
  },
  methods: {
    fetchXml(url) {
      fetch(url)
        .then((res) => res.text())
        .then((txt) => this.parseXML(txt))
        .catch((err) => (this.errorMessage = err));
    },
    parseXML(txt) {
      let xmlDoc = new DOMParser().parseFromString(txt, "text/xml");
      let items = xmlDoc.getElementsByTagName("item");
      let news = [];
      items.forEach((item) => {
        news.push({
          title: getFirst(item, "title"),
          link: getFirst(item, "link"),
          dcCreator: getFirst(item, "dc:creator", "No Creator"),
          description: getFirst(item, "description", "No Description"),
          pubDate: getFirst(item, "pubDate"),
          credit: getFirst(item, "media:credit", "No Credit"),
          image: getAttr(item, "media:content", "url", null),
          categories: getAllItem(item, "category", "[]"),
        });
      });
      this.newsList = news;
    },
    changeCategory(category) {
      this.errorMessage = "";
      this.activeCategory = category.id;
      this.xmlUrl = `https://rss.nytimes.com/services/xml/rss/nyt/${category.url}.xml`;
      this.fetchXml(this.xmlUrl);
      document.documentElement.scrollTop = 0;
    },
  },
};
</script>

<style scoped>
.sticky {
  position: sticky;
  top: 0;
}
.columns {
  margin-left: 0.1px;
  margin-right: 0.1px;
}
</style>
