<template>
  <div>
    <div class="header">
      <ul class="header-button-left">
        <li>Cancel</li>
      </ul>
      <ul class="header-button-right">
        <li v-if="tapState == 2">Next</li>
        <li v-if="tapState == 3">발행</li>
      </ul>
      <img @click="tapState = 1" src="./assets/logo.png" class="logo" />
    </div>

    <Container :boards="boards" :tapState="tapState" :imgUrl="imgUrl" />

    <!-- 클릭시 axios를 이용해 받은 데이터를 기존 데이터 배열에 추가하는 함수가 실행됨 -->
    <button @click="onClickMore">더보기</button>

    <div class="footer">
      <ul class="footer-button-plus">
        <input type="file" @change="uploadImg" id="file" class="inputfile" />
        <label for="file" class="input-plus">+</label>
      </ul>
    </div>
  </div>
</template>

<script>
import Container from "./components/Container.vue";
import boards from "./data/boards";
import axios from "axios";

export default {
  name: "App",
  components: {
    Container,
  },
  data() {
    return {
      boards,
      moreCount: 0,
      tapState: 1,
      imgUrl: "",
    };
  },
  methods: {
    onClickMore() {
      axios
        .get(
          "https://codingapple1.github.io/vue/more" + this.moreCount + ".json"
        )
        .then((result) => {
          console.log(result);

          // 글목록 데이터(배열)에 GET받은 데이터를 추가함
          this.boards.push(result.data);

          // this.moreCount++;
          this.moreCount = this.moreCount + 1;
        })
        .catch(() => {
          alert("게시물이 없음!! (catch)");
        });
    },
    uploadImg(event) {
      let img = event.target.files;
      console.log(img[0]);
      this.imgUrl = URL.createObjectURL(img[0]);
      console.log(this.imgUrl);
      this.tapState++;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
