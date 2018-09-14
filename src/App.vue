<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-4 input-group">
        <my-selector @my-select-change="getCity" v-model="city" :items="sourceCities"></my-selector>
      </div>
      <div class="col-md-4 input-group">
        <my-selector @my-select-change="getDistrict" v-model="district" :items="sourceDist"
                     :value="district"></my-selector>
      </div>
      <div class="col-md-4">
        <span>{{zip}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import MySelector from './components/MySelector.vue';
import { API } from './env';

export default {
  name: 'app',
  components: {
    MySelector,
  },
  data() {
    return {
      city: 0,
      district: 0,
      cities: [
        {
          name: '',
          areas: [
            {
              name: '',
              zip: '',
            },
          ],
        }],
      zip: '',
      url: API,
      error: '',
      isLoad: false,
    };
  },
  created() {
    console.log('ajax 底加拉');
    console.log(this.url);

    const response = (res) => {
      console.log(res.data);
      //
      if (res.status === 200) {
        this.cities = res.data;
      } else {
        this.error = 'data source';
      }
    };

    const error = e => console.log(e);

    axios
      .post(this.url)
      .then(response)
      .catch(error);
  },
  computed: {
    sourceCities() {
      this.getZip(0);
      return this.cities;
    },
    sourceDist() {
      return this.cities[this.city].areas;
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
      this.zip = this.cities[this.city].areas[value].zip;
    },
  },
  watch: {
    city() {
      this.district = 0;
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
