<template>
  <select class="form-control" @change="exportSelected" v-model="select">
    <option v-for="(item, index) in items" :value="index" :key="index">{{item.name}}</option>
  </select>
</template>

<script>

export default {
  name: 'MySelector',
  props: {
    value: Number,
    items: Array,
  },
  data() {
    return {
      select: 0,
    };
  },
  methods: {
    exportSelected() {
      this.$emit('my-select-change', this.select);
    },
  },
  watch: {
    value() {
      this.select = this.value;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
