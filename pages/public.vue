<template>
  <div class="mx-auto">
    <h2 class="font-bold text-3xl text-center mt-10">Halaman Public</h2>
    <p class="text-center my-5">
      Free access to open album, search and filter pic
    </p>
    <div class="flex flex-row justify-between">
      <Search v-on:keyword="getKeyword" />
      <Filters v-on:filter="getFilter" />
    </div>

    <div class="grid grid-cols-4 gap-4 px-8" v-if="!isShowPhoto">
      <div v-for="album in albumData" :key="album.id">
        <div
          class="flex flex-col cursor-pointer"
          v-on:click="onAccessAlbum(album.albumId)"
        >
          <img src="~/assets/liberty.jpg" class="rounded-xl" alt="" />
          <p class="text-center">Photo Album {{ album.albumId }}</p>
        </div>
      </div>
    </div>

    <div class="grid grid-cols-4 gap-4 px-8" v-if="isShowPhoto">
      <div v-for="photo in photoData" :key="photo.id">
        <div class="flex flex-col cursor-pointer">
          <img :src="photo.thumbnailUrl" class="rounded-xl" alt="" />
          <p class="text-center">Photo Album {{ photo.title }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Search from "../components/Search.vue";
import Filters from "../components/Filters.vue";
import axios from "axios";

export default Vue.extend({
  components: { Search, Filters },
  name: "UsersPage",

  data() {
    return {
      photoData: [] as any,
      albumData: [] as any,
      isShowPhoto: false,
      keyword: "",
      accessAlbum: 0,
      filter: "",
      page: 1,
    };
  },

  mounted() {
    console.log(this.page);
    this.getPhotoData();
  },

  methods: {
    getPhotoData() {
      axios
        .get("http://localhost:8200/api/public/album/?skip=0&limit=10")
        .then((response: any) => {
          console.log(response);
          this.albumData = response.data.albums;
        });
    },

    onAccessAlbum(accessAlbum: number) {
      this.accessAlbum = accessAlbum;
      axios
        .get(
          `http://localhost:8200/api/public/album/${accessAlbum}?sort=${this.filter}&skip=0&limit=10&title=${this.keyword}`
        )
        .then((response: any) => {
          console.log(response);
          this.isShowPhoto = true;
          this.photoData = response.data.photos;
        });
    },

    getKeyword(val: string) {
      this.keyword = val;
      this.onAccessAlbum(this.accessAlbum);
    },

    getFilter(val: string) {
      console.log("heres", val);
      this.filter = val;
      this.onAccessAlbum(this.accessAlbum);
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
