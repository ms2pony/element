<template>
  <el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
</template>

<script>
  export default {
    data() {
      return {
        options: new Array(20).fill(0).map((v, idx) => {
        return {
          value: idx,
          label: `第${idx + 1}个`,
        };
      }),
        value: ''
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>