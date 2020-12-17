<template>
  <div class="container mx-auto p-2">
    <!-- TODO put into separate headline component -->
    <h1 class="text-5xl mb-2 md:mb-4">spectrm-challenge</h1>

    <div v-if="profiles" class="flex flex-col xl:flex-row xl:space-x-2">
      <div v-for="(profile, index) in profiles" :key="index" class="w-1/2">
        <ChartCard
          :title="profile.title"
          :total-label="profile.totalLabel"
          :data="profile.original"
          class="mb-4"
          :can-clone="!profile.clone"
          @clone="onClone"
        />
        <ChartCard
          v-if="profile.clone"
          :title="profile.title + ' clone'"
          :total-label="profile.totalLabel"
          :data="profile.clone"
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
    const profiles = data.profiles.map((profile: any) => {
      return {
        title: profile.title,
        totalLabel: profile.totalLabel,
        original: {
          series: profile.data.map((seriesLabel: any) => seriesLabel.value),
          labels: profile.data.map((seriesLabel: any) => seriesLabel.label)
        },
        clone: null
      };
    });
    return { profiles };
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
      profiles: null
    };
  },
  methods: {
    onClone(profileTitle: string) {
      // @ts-ignore
      const index = this.profiles.findIndex(
        (profile: any) => profile.title === profileTitle
      );
      // @ts-ignore
      const profile = this.profiles[index];
      // make deep copies
      profile.clone = {
        series: JSON.parse(JSON.stringify(profile.original.series)),
        labels: JSON.parse(JSON.stringify(profile.original.labels))
      };
      // @ts-ignore
      this.profiles[index] = profile;
    }
  }
});
</script>

<style></style>
