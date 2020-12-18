<template>
  <div class="chart-card shadow-lg rounded-md bg-white">
    <div class="flex flex-row justify-between px-4 pt-4">
      <h1
        class="text-lg font-sans font-semibold border-b-2 border-dotted border-gray-500"
      >
        {{ title }}
      </h1>
      <CloneOption v-if="canClone" @clone="onClone" />
    </div>
    <DonutChart
      class="w-full"
      :series="data.series"
      :labels="data.labels"
      :total-label="totalLabel"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    title: {
      type: String,
      required: true
    },
    totalLabel: {
      type: String,
      required: true
    },
    data: {
      type: Object,
      required: true
    },
    canClone: {
      type: Boolean
    }
  },
  methods: {
    onClone() {
      // @ts-ignore
      this.$emit("clone", this.title);
    }
  }
});
</script>

<style>
.chart-card {
  min-height: 250px;
}
</style>
