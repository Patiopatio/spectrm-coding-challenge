<template>
  <div class="min-w-full min-h-full bg-red shadow-lg rounded-md bg-white">
    <div class="flex flex-row justify-between px-4 pt-4">
      <h1 class="font-sans font-semibold border-b-2 border-dotted">
        {{ profile.title }}
      </h1>
      <CloneOption />
    </div>
    <!-- max-w-xs md:max-w-md lg:max-w-lg -->
    <DonutChart
      class="w-full"
      :series="series"
      :labels="labels"
      :total-label="profile.totalLabel"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    profile: {
      type: Object,
      required: true
    }
  },
  computed: {
    series() {
      return this.profile.data.map((d: any) => d.value);
    },
    labels() {
      return this.profile.data.map((d: any) => d.label);
    }
  }
});
</script>

<style></style>
