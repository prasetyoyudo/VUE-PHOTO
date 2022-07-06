<template>
  <div>
    <div class="pr-8 pt-4">
      <div class="dropdown inline-block relative">
        <button
          class="bg-gray-300 text-gray-700 font-semibold py-2 px-4 rounded inline-flex items-center"
        >
          <span class="mr-1">Filter Album</span>
          <svg
            class="fill-current h-4 w-4"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
          >
            <path
              d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
            />
          </svg>
        </button>
        <ul class="dropdown-menu absolute hidden text-gray-700 pt-1 w-full">
          <li class="" v-on:click="onFilterUser('ASC')">
            <span
              class="rounded-t bg-gray-200 hover:bg-gray-400 py-2 px-4 block whitespace-no-wrap cursor-pointer"
              href="#"
              >Ascending</span
            >
          </li>
          <li class="">
            <span
              v-on:click="onFilterUser('DESC')"
              class="bg-gray-200 hover:bg-gray-400 py-2 px-4 block whitespace-no-wrap cursor-pointer"
              href="#"
              >Descending</span
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default {
  name: "FilterPage",

  data() {
    return {};
  },

  mounted() {
    // this.getUsersData();
  },

  methods: {
    onFilterUser(event: string) {
      console.log(event);
      this.$emit('filter', event);
    },
  },
};
</script>

<style>
.dropdown:hover .dropdown-menu {
  display: block;
}
</style>
