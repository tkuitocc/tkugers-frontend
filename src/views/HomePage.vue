<template>
  <div>
    <input
      class="classSearch_input"
      v-model="inputData"
      type="text"
      @input="onSearch"
    />
    <ul>
      <li v-for="itemObj in searchResult" :key="itemObj.refIndex">
        {{ itemObj.item.className }}
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
  },
};
</script>

<style lang="scss" scoped></style>
