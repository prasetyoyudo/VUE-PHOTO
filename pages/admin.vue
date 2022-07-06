<template>
  <div class="flex flex-col mx-10 my-10 space-y-6">
    <h1 class="text-3xl font-serif text-center">Halaman Admin</h1>
    <div class="flex justify-between">
      <!-- untuk filter search -->
      <div></div>
      <!-- add image -->
      <button
        class="px-4 py-2 text-center space-x-1 rounded-2xl bg-blue-700 text-white"
        v-on:click="showAddImage = true"
      >
        + Tambah Gambar
      </button>
    </div>

    <!-- form add -->
    <div
      class="flex flex-col justify-center items-center space-y-4"
      v-if="showAddImage"
    >
      <!-- input title image -->
      <div class="flex space-x-2 items-center">
        <p class="text-lg">Title :</p>
        <input
          type="text"
          class="rounded-lg border border-1 border-green-300 px-3 py-2"
          placeholder="masukkan judul gambar"
          v-model="formRequest.title"
        />
      </div>
      <!-- input url image -->
      <div class="flex space-x-2 items-center">
        <p class="text-lg">Url Gambar :</p>
        <input
          type="text"
          class="rounded-lg border border-1 border-green-300 px-3 py-2"
          placeholder="masukkan url gambar"
          v-model="formRequest.url"
        />
      </div>
      <!-- input album type -->
      <div class="flex space-x-2 items-center">
        <p class="text-lg">Album :</p>
        <select
          v-model="formRequest.albumId"
          class="rounded-lg border border-1 border-green-300 px-3 py-2"
        >
          <option value="">Pilih Album</option>
          <option v-for="item in 50" :key="item" :value="item">
            Album ~ {{ item }}
          </option>
        </select>
      </div>

      <button
        class="px-4 py-2 bg-blue-700 text-white rounded-3xl"
        v-on:click="submitData()"
      >
        Submit
      </button>
    </div>

    <div
      class="grid grid-cols-2 gap-8 w-full"
      v-if="imageList.length !== 0 && !showAlbum"
    >
      <div
        v-for="img in imageList"
        :key="img.id"
        class="flex space-x-2 border-1 shadow-lg rounded-md bg-white p-4 w-full curs"
      >
        <img :src="img.url" alt="" width="200px" height="200px" />
        <div class="flex flex-col space-y-4">
          <p class="text-xl capitalize">
            {{ img.title }}
          </p>
          <div class="flex space-x-2">
            <button
              class="text-center px-4 py-2 rounded-md text-white bg-yellow-400 text-nowrap"
            >
              Ubah Nama Gambar
            </button>
            <button
              class="text-center px-4 py-2 rounded-md text-white bg-red-500 text-nowrap"
              v-on:click="deletePhoto(img.id, img.albumId)"
            >
              Hapus Gambar
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- list album -->
    <div
      class="grid grid-cols-2 gap-8 w-full"
      v-if="albumList.length !== 0 && showAlbum"
    >
      <div
        v-for="img in albumList"
        :key="img.id"
        class="flex space-x-2 border-1 shadow-lg rounded-md bg-white p-4 w-full cursor-pointer"
      >
        <img
          src="~/assets/liberty.jpg"
          alt=""
          class="cursor-pointer"
          width="200px"
          height="200px"
          v-on:click="showListPhoto(img.albumId)"
        />
        <div class="flex flex-col space-y-4">
          <p class="text-xl capitalize">Album {{ img.albumId }}</p>
          <div class="flex space-x-2">
            <button
              class="text-center px-4 py-2 rounded-md text-white bg-yellow-400 text-nowrap"
            >
              Ubah Nama Gambar
            </button>
            <button
              class="text-center px-4 py-2 rounded-md text-white bg-red-500 text-nowrap"
              v-on:click="deleteAlbum(img.albumId)"
            >
              Hapus Album
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
interface ImageInterface {
  id: string;
  title: string;
  url: string;
  albumId: number;
}
import Vue from "vue";
import ListImage from "../components/ListImage.vue";
import ListAlbum from "../components/ListAlbum.vue";
import axios from "axios";
import { PropType } from "vue/types/v3-component-props";
export default Vue.extend({
  name: "AdminPage",
  components: { ListImage, ListAlbum },

  data() {
    return {
      imageList: [] as ImageInterface[],
      albumList: [] as ImageInterface[],
      formRequest: {
        title: "",
        url: "",
        albumId: "",
      },
      showAddImage: false,
      showAlbum: true,
      idSelected: 1,
    };
  },
  mounted() {
    this.getListAlbum("ASC");
  },

  methods: {
    getListAlbum(sort: string) {
      const url = `http://localhost:8200/api/public/album?sort=${sort}&skip=0&limit=20`;
      axios.get(url).then((res) => {
        this.albumList = res.data.albums;
      });
    },
    getListImage(sort: string, albumId: number) {
      const url = `http://localhost:8200/api/public/album/${albumId}?sort=${sort}&skip=0&limit=20`;
      axios.get(url).then((res) => {
        this.imageList = res.data.photos;
      });
    },

    submitData() {
      const body = {
        albumId: +this.formRequest.albumId,
        title: this.formRequest.title,
        url: this.formRequest.url,
        thumbnailUrl: this.formRequest.url,
      };
      const url = "http://localhost:8200/api/admin/photo";
      axios.post(url, body).then((res) => {
        this.showAddImage = false;
        this.getListImage("DESC", body.albumId);
        alert("Photo berhasil ditambahkan");
      });
    },

    showListPhoto(albumId: number) {
      this.showAlbum = false;
      this.getListImage("ASC", albumId);
    },

    deleteAlbum(albumId: number) {
      const url = `http://localhost:8200/api/admin/album/${albumId}`;
      axios.delete(url).then((res) => {
        alert(`Album telah dihapus`);
        this.getListAlbum("ASC");
      });
    },

    deletePhoto(photoId: string, albumId: number) {
      const url = `http://localhost:8200/api/admin/photo/${photoId}`;
      axios.delete(url).then((res) => {
        alert(`Photo telah dihapus`);
        this.getListImage("ASC", albumId);
      });
    },
  },
});
</script>

<style>
input:focus {
  border: 0px solid transparent !important;
}
input {
  width: 250px;
}
</style>
