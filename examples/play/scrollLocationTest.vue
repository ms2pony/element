<template>
  <div>
    <button @click="setLocation(options, 14, scrollContainer)">我们</button>
    <!-- <el-select v-model="value" placeholder="请选择">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select> -->
    <div class="scrollContainer">
      <ul>
        <li :key="i" v-for="(v, i) in options">{{ v.label }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    setLocation(items, idx, scrollContainer) {
      let itemOffset =
        ((idx + 1) / items.length) * scrollContainer.scrollHeight;
      let itemPosition = itemOffset - scrollContainer.scrollTop;
      let mediumHeight = scrollContainer.clientHeight / 2;

      if (itemPosition < mediumHeight) {
        let tmp = scrollContainer.scrollTop - (mediumHeight - itemPosition);
        scrollContainer.scrollTop = tmp < 0 ? 0 : tmp;
      } else {
        let tmp = scrollContainer.scrollTop + (itemPosition - mediumHeight);
        scrollContainer.scrollTop =
          tmp > scrollContainer.scrollHeight
            ? scrollContainer.scrollHeight
            : tmp;
      }

      // 高亮当前元素, 然后又消失
      const selectItem = scrollContainer.firstChild.children[idx];
      selectItem.classList.add("highlight");
      // requestAnimationFrame(() => {
      //   selectItem.classList.remove("highlight");
      // });
      setTimeout(()=>{
        selectItem.classList.remove("highlight");
      },1000)
    },
  },
  mounted() {
    this.$nextTick(() => {
      this.scrollContainer = document.querySelector(".scrollContainer");
    });
  },
  data() {
    return {
      // options: [
      //   {
      //     value: "选项1",
      //     label: "黄金糕",
      //   },
      //   {
      //     value: "选项2",
      //     label: "双皮奶",
      //   },
      //   {
      //     value: "选项3",
      //     label: "蚵仔煎",
      //   },
      //   {
      //     value: "选项4",
      //     label: "龙须面",
      //   },
      //   {
      //     value: "选项5",
      //     label: "北京烤鸭",
      //   },
      //   {
      //     value: "选项6",
      //     label: "黄金糕",
      //   },
      //   {
      //     value: "选项7",
      //     label: "双皮奶",
      //   },
      //   {
      //     value: "选项8",
      //     label: "蚵仔煎",
      //   },
      //   {
      //     value: "选项9",
      //     label: "龙须面",
      //   },
      //   {
      //     value: "选项10",
      //     label: "北京烤鸭",
      //   },
      //   {
      //     value: "选项11",
      //     label: "黄金糕",
      //   },
      //   {
      //     value: "选项12",
      //     label: "双皮奶",
      //   },
      //   {
      //     value: "选项13",
      //     label: "蚵仔煎",
      //   },
      //   {
      //     value: "选项14",
      //     label: "龙须面",
      //   },
      //   {
      //     value: "选项15",
      //     label: "北京烤鸭",
      //   },
      // ],
      options: new Array(20).fill(0).map((v, idx) => {
        return {
          value: idx,
          label: `第${idx + 1}个`,
        };
      }),
      value: "",
    };
  },
};
</script>
<style  scoped>
.scrollContainer {
  width: 200px;
  height: 230px;
  overflow: auto;
}
</style>
<style lang="scss" scoped>
.scrollContainer{
  li{
    transition: background-color 1s;
  }
  li.highlight{
    background-color: yellow;
  }
}
</style>