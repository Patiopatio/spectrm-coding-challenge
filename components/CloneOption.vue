<template>
  <div class="relative">
    <button
      @click="isOpen = !isOpen"
      class="block h-6 w-6 md:h-8 md:w-8 rounded-full overflow-hidden focus:outline-none"
    >
      <img
        class="h-full w-full object-cover"
        src="~/assets/option.png"
        alt=""
      />
    </button>
    <div
      v-if="isOpen"
      class="absolute right-0 mt-2 py-2 bg-white border rounded shadow-xl z-10"
    >
      <span
        @click="onClickClone"
        class="transition-colors duration-200 block px-4 py-2 text-normal text-gray-900 rounded hover:bg-purple-500 hover:text-white"
        >Clone</span
      >
    </div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return { isOpen: false };
  },
  methods: {
    onClickClone() {
      this.$emit("clone-profile");
    }
  }
});
</script>
