<template>
  <div class="container mx-auto p-2">
    <h1 class="text-5xl mb-2 md:mb-4 text-center">spectrm-challenge</h1>

    <img
      src="~assets/challenge.gif"
      alt="Challenge accepted"
      class="mx-auto w-full md:w-72 rounded-lg overflow-hidden mb-2"
    />

    <div v-if="profiles" class="flex flex-col xl:flex-row flex-wrap">
      <div
        v-for="(profile, index) in profiles"
        :key="index"
        class="card"
        :class="{ 'xl:mx-2': index % 3 == 1 }"
      >
        <ChartCard
          :title="profile.title"
          :total-label="profile.totalLabel"
          :data="profile.original"
          class="mb-2"
          @clone="onClone"
          :index="index"
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
    const profiles = data.profiles.map((profile: any) => {
      return {
        title: profile.title,
        totalLabel: profile.totalLabel,
        original: {
          series: profile.data.map((seriesLabel: any) => seriesLabel.value),
          labels: profile.data.map((seriesLabel: any) => seriesLabel.label)
        }
      };
    });
    return { profiles };
  },
  data() {
    return {
      profiles: null
    };
  },
  methods: {
    onClone(index: number) {
      // @ts-ignore
      const profile = JSON.parse(JSON.stringify(this.profiles[index]));
      // @ts-ignore
      this.profiles.push(profile);
    }
  }
});
</script>

<style>
.card  {
  flex: 1;
}
@media (min-width: 768px) {
  .card {
    flex: 0 32%;
  }
}
</style>
