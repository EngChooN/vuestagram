<template>
  <div>
    <div v-if="tapState == 1">
      <Post v-for="(el, index) in boards" :key="index" :elBoards="el" />
    </div>

    <!-- 필터선택페이지 -->
    <div v-if="tapState == 2">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imgUrl})` }"
      ></div>
      <div class="filters">
        <!-- <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div> -->
        <FilterBox
          v-for="(el, index) in filters"
          :key="index"
          :imgUrl="imgUrl"
          :filters="el"
        />
      </div>
    </div>

    <!-- 글작성페이지. -->
    <div v-if="tapState == 3">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imgUrl})` }"
      ></div>
      <div class="write">
        <textarea
          class="write-box"
          placeholder="write text!"
          @change="onChangeContent"
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "./Post.vue";
import FilterBox from "./FilterBox.vue";

export default {
  name: "ContainerComponent",
  components: {
    Post,
    FilterBox,
  },
  props: {
    boards: Array,
    tapState: Number,
    imgUrl: String,
    myContent: String,
  },
  methods: {
    onChangeContent(e) {
      this.$emit("onChangeContent", e.target.value);
    },
  },
  data() {
    return {
      filters: [
        "aden",
        "_1977",
        "brannan",
        "brooklyn",
        "clarendon",
        "earlybird",
        "gingham",
        "hudson",
        "inkwell",
        "kelvin",
        "lark",
        "lofi",
        "maven",
        "mayfair",
        "moon",
        "nashville",
        "perpetua",
        "reyes",
        "rise",
        "slumber",
        "stinson",
        "toaster",
        "valencia",
        "walden",
        "willow",
        "xpro2",
      ],
    };
  },
};
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>
