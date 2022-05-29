<template>
  <div class="homepage">
    <div class="homepage-titleBox">
      <div class="homepage-titleBox_title">淡江大學選課推薦系統</div>
      <div class="homepage-titleBox_copyright">Copyright form TKUAIIC</div>
      <div class="homepage-titleBox_subTitle">
        Tamkang University className Selection Recommendation System
      </div>
    </div>
    <div class="homepage-searchBox">
      <div class="homepage-searchBox_autocomplete">
        <input
          class="homepage-searchBox_input"
          v-model="inputData"
          type="text"
          @input="onSearch"
          placeholder="請輸入您想查詢的課程"
        />
        <ul class="homepage-searchBox_autocompleteItem">
          <li v-for="itemObj in searchResult" :key="itemObj.refIndex">
            {{ itemObj.item.className }}
          </li>
        </ul>
      </div>
      <button class="homepage-searchBox_button" @click="submitSearch">
        搜尋
      </button>
    </div>
    <ul class="homepage-resultBox">
      <li
        class="homepage-resultBox_item"
        v-for="itemObj in submitSearchResult"
        :key="itemObj.id"
      >
        {{ itemObj.className }}
      </li>
    </ul>
  </div>
</template>

<script>
import Fuse from "fuse.js";

export default {
  data() {
    return {
      inputData: "",
      searchResult: [],
      submitSearchResult: [],
      fakeClassData: [
        { id: 1, className: "計算機概論" },
        { id: 2, className: "管理資訊系統" },
        { id: 3, className: "Web程式設計" },
        { id: 4, className: "行動裝置程式設計" },
        { id: 5, className: "Python資料分析" },
        { id: 6, className: "資料結構" },
        { id: 7, className: "演算法" },
        { id: 8, className: "資料庫" },
        { id: 9, className: "作業系統" },
        { id: 10, className: "專題實驗" },
        {
          id: "F50890606",
          className: "日本名家名著中譯賞析",
        },
        {
          id: "F50890606",
          className: "義大利文與文化",
        },
        {
          id: "D40890606",
          className: "專家詩",
        },
        {
          id: "D40890606",
          className: "古典長篇小說選",
        },
        {
          id: "D40890606",
          className: "兒童文學",
        },
        {
          id: "D40890606",
          className: "教學媒體與運用",
        },
        {
          id: "D40890606",
          className: "行政學",
        },
        {
          id: "D40890606",
          className: "行政法",
        },
        {
          id: "D40890606",
          className: "職業教育與訓練",
        },
        {
          id: "D40890606",
          className: "中學實地學習",
        },
        {
          id: "D40890606",
          className: "適性教學",
        },
        {
          id: "B30890606",
          className: "電影與文學",
        },
        {
          id: "B30890606",
          className: "編輯與出版",
        },
        {
          id: "B30890606",
          className: "文藝編輯學",
        },
        {
          id: "B30890606",
          className: "韓文（一）",
        },
        {
          id: "B30890606",
          className: "華語文教材教法",
        },
        {
          id: "B30890606",
          className: "文藝編輯學",
        },
        {
          id: "B30890606",
          className: "運動休閒與競技實務─彼拉提斯",
        },
        {
          id: "B30890606",
          className: "森林生態與樹木保護",
        },
        {
          id: "J20890606",
          className: "中國現代文學史",
        },
        {
          id: "J20890606",
          className: "曲學通論",
        },
        {
          id: "J20890606",
          className: "漢學英文",
        },
        {
          id: "J20890606",
          className: "電影美學",
        },
        {
          id: "J20890606",
          className: "英作文（二）",
        },
        {
          id: "J20890606",
          className: "英語口語表達",
        },
        {
          id: "J20890606",
          className: "英國文學（二）",
        },
        {
          id: "J20890606",
          className: "策略管理",
        },
        {
          id: "J20890606",
          className: "現代詩及習作",
        },
        {
          id: "J20890606",
          className: "中國現代文學史",
        },
        {
          id: "H10890606",
          className: "古典長篇小說選",
        },
        {
          id: "H10890606",
          className: "資古典長篇小說選",
        },
        {
          id: "H108902136",
          className: "資古典長篇小說選",
        },
      ],
    };
  },
  methods: {
    onSearch() {
      const options = {
        includeScore: true,
        keys: ["className"],
      };
      const fuse = new Fuse(this.fakeClassData, options);
      const result = fuse.search(this.inputData);

      this.searchResult = result;
    },
    submitSearch() {
      this.submitSearchResult = [];
      let result = [];
      for (let i = 0; i < 6; i++) {
        const index = Math.floor(Math.random() * this.fakeClassData.length);
        result.push(this.fakeClassData[index]);
      }
      this.submitSearchResult = result;
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Lustria&display=swap");

.homepage {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
  background-color: #f4fbff;
  min-height: 100vh;

  .homepage-titleBox {
    width: 100%;
    margin-top: 85px;
    text-align: center;

    .homepage-titleBox_title {
      font-family: "Lustria", serif;
      font-size: 24px;
      color: #355c65;
      font-weight: 600;
      letter-spacing: 0.15em;
    }

    .homepage-titleBox_subTitle {
      font-family: "Lustria";
      font-size: 15px;
      color: #84979b;
      letter-spacing: 0.09em;
      margin-bottom: 32px;
    }

    .homepage-titleBox_copyright {
      font-family: "Lustria";
      font-weight: 400;
      font-size: 8px;
      letter-spacing: 0.09em;
      color: #cdcfcf;
      margin-bottom: 13px;
    }
  }

  .homepage-searchBox {
    width: 100%;
    display: flex;
    justify-content: center;

    .homepage-searchBox_autocomplete {
      width: 35%;
      position: relative;

      .homepage-searchBox_autocompleteItem {
        width: 100%;
        position: absolute;
        list-style: none;
        z-index: 10;

        li {
          width: 100%;
          margin-right: 12px;
          border: none;
          font-size: 16px;
          color: #afafaf;
          padding: 10px 24px;
          font-weight: 600;
          border-radius: 4px;
          letter-spacing: 0.15em;
          background-color: white;
        }
      }
    }

    .homepage-searchBox_input {
      width: 100%;
      height: 45px;
      margin-right: 12px;
      border: none;
      font-size: 16px;
      color: #afafaf;
      padding-left: 24px;
      font-weight: 600;
      border-radius: 4px;
      letter-spacing: 0.15em;

      &:focus {
        outline: none;
      }
    }

    .homepage-searchBox_button {
      width: 70px;
      height: 45px;
      border: none;
      background: rgba(78, 111, 109, 0.66);
      border-radius: 4px;
      font-family: "Lustria";
      font-weight: 600;
      font-size: 16px;
      color: #f4fbff;
    }
  }

  .homepage-resultBox {
    padding: 65px 345px;
    list-style: none;
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;

    .homepage-resultBox_item {
      filter: drop-shadow(2px 2px 40px rgba(0, 0, 0, 0.1));
      border-radius: 15px;
      width: 300px;
      height: 128px;
      padding: 15px;
      margin: 35px 35px;
      background: linear-gradient(
        to right,
        rgba(253, 252, 255, 0.86) 75%,
        rgba(85, 194, 255, 0.07) 75%
      );
      font-family: "Lustria";
      font-weight: 600;
      font-size: 16px;
      color: #afafaf;
    }
  }
}
</style>
