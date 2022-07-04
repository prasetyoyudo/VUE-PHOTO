<template>
  <div>
    <div class="grid grid-cols-4 gap-4 px-4">
      <div class="flex flex-col cursor-pointer" v-on:click="onAccessAlbum('user')">
        <img src="~/assets/liberty.jpg" class="" alt="" />
        <p class="text-center">Album 1</p>
      </div>
      <div class="flex flex-col cursor-pointer"  v-on:click="onAccessAlbum('user')">
        <img src="~/assets/liberty.jpg" class="" alt="" />
        <p class="text-center">Album 2</p>
      </div>
      <div class="flex flex-col cursor-pointer" v-on:click="onAccessAlbum('user')">
        <img src="~/assets/liberty.jpg" class="" alt="" />
        <p class="text-center">Album 3</p>
      </div>
      <div class="flex flex-col cursor-pointer" v-on:click="onAccessAlbum('user')">
        <img src="~/assets/liberty.jpg" class="" alt="" />
        <p class="text-center">Album 4</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
// import  AdminPage  from './admin/Admin.vue'

export default Vue.extend({
  name: "UsersPage",

  data() {
    return {};
  },

  mounted() {
    // this.getUsersData();
  },

  methods: {
    onAccessAlbum(access: string) {
      console.log(access);
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
