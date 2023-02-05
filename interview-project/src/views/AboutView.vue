<template>
  <div class="about">
    <van-search
      v-model="value"
      placeholder="请输入搜索关键词"
      clearable
      @search="onSearch"
    />
    <van-tree-select
      :items="items"
      :active-id.sync="activeId"
      :main-active-index.sync="activeIndex"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      items:[{ text: '类型一',id:1},{ text: '类型二',id:2},{ text: '类型三',id:3}],
      activeId: 1,
      activeIndex: 0,
    };
  },
  method: {
    onSearch() {},
  },
};
</script>

