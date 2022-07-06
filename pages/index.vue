<template>
  <div class="container mx-auto">
    <h2 class="font-bold text-3xl text-center mt-10">Photo Management</h2>
    <p class="text-center mt-8">Dummy landing page for photo management, you can access via user or admin as you want</p>
    <div class="flex flex-row mx-auto text-center w-6/12 justify-between mt-10">
      <button
        class="py-1 rounded-full w-4/12 user text-white font-semibold"
        v-on:click="onAccessPage('public')"
      >
        Login Via Public
      </button>
      <button
        class="py-1 rounded-full w-4/12 admin text-white font-semibold"
        v-on:click="onAccessPage('admin')"
      >
        Login Via Admin
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage",

  data() {
    return {};
  },

  mounted() {
    // this.getUsersData();
  },

  methods: {
    onAccessPage(access: string) {
        this.$router.push(`/${access}`)
    },
  },
});
</script>

<style>
.user {
  background-color: #00d8d6;
}

.admin {
  background-color: #ff5e57;
}
</style>
