<template>
  <div class="relative">
    <button
      @click="isOpen = !isOpen"
      class="block h-4 w-4 md:h-6 md:w-6 rounded-full overflow-hidden focus:outline-none"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-three-dots-vertical h-full w-full object-cover"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M9.5 13a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0z"
        />
      </svg>
    </button>
    <div
      v-if="isOpen"
      class="z-10 absolute right-0 mt-2 border rounded shadow-xl bg-white"
    >
      <span
        @click="onClickClone"
        class="cursor-pointer transition-colors duration-200 block px-4 py-2 text-normal text-gray-900 rounded hover:bg-gray-400 hover:text-white"
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
      this.$emit("clone");
      this.isOpen = !this.isOpen;
    }
  }
});
</script>
