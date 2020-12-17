<template>
  <div
    class="container m-auto h-full px-4 md:px-16 w-full md:w-1/2 bg-gray-100"
  >
    <div class="flex justify-center items-center">
      <div>
        <h1 class="title">spectrm-challenge</h1>
        <ChartCard
          v-for="(profile, index) in profiles"
          :key="index"
          :profile="profile"
          class="mb-4"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import data from "~/static/data.json";

export default Vue.extend({
  async asyncData({ req, isServer, params, store }) {
    console.log(data);
    return { profiles: data.profiles };
    // const data = {
    //   charts: null,
    // };

    // if (process.server) {
    //   data.charts = JSON.parse(
    //     require("fs").readFileSync("../static/data.json", "utf8")
    //   );
    // } else {
    //   // data.charts = await axios.get('/data.json').then(res => res.data)
    // }

    // console.log(data);

    // return data;
  },
  data() {
    return {
      profiles: []
    };
  }
});
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
