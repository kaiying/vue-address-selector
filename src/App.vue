<template>
  <div id="app" class="container">
    <div class="row">
    <div class="col-md-4 input-group">
          <my-selector @my-select-change="getCity" v-model="city" v-bind:items="cities"></my-selector>
    </div>
    <div class="col-md-4 input-group">
    <my-selector @my-select-change="getDistrict" :value="changeDist" v-bind:items="dist"></my-selector>
    </div>
    <div class="col-md-4">
    <span>{{zip}}</span>
    </div>
    </div>
  </div>
</template>

<script>

import MySelector from './components/MySelector.vue';

const cities = [
  {
    name: '基隆市',
    areas: [
      { name: '仁愛區', zip: '200' },
      { name: '信義區', zip: '201' },
      { name: '中正區', zip: '202' },
      { name: '中山區', zip: '203' },
      { name: '安樂區', zip: '204' },
      { name: '暖暖區', zip: '205' },
      { name: '七堵區', zip: '206' },
    ],
  },
  {
    name: '台北市',
    areas: [
      { name: '中正區', zip: '300' },
      { name: '大同區', zip: '301' },
      { name: '中山區', zip: '302' },
      { name: '松山區', zip: '303' },
      { name: '大安區', zip: '304' },
      { name: '萬華區', zip: '305' },
      { name: '信義區', zip: '306' },
      { name: '士林區', zip: '307' },
      { name: '北投區', zip: '308' },
      { name: '內湖區', zip: '309' },
      { name: '南港區', zip: '310' },
      { name: '文山區', zip: '311' },
    ],
  },
  {
    name: '新竹市',
    areas: [
      { name: '新竹市', zip: '400' },
    ],
  },
];

export default {
  name: 'app',
  components: {
    MySelector,
  },
  data() {
    return {
      city: 0,
      district: 0,
      sub: 0,
      cities,
      dist: cities,
      zip: '',
    };
  },
  computed: {
    changeDist() {
      this.dist = cities[this.city].areas;
      this.district = 0;
      this.getZip(0);
      return this.city;
    },
  },
  methods: {
    getCity(value) {
      this.city = value;
    },
    getDistrict(value) {
      this.district = value;
      this.getZip(value);
    },
    getZip(value) {
      this.zip = this.dist[value].zip;
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
