<template>
  <div class="container">
    <h2 class="font-bold text-3xl text-center mt-10">Photo Management</h2>
    <div class="flex flex-row mx-auto text-center w-6/12 justify-between mt-10">
      <button
        class="py-1 rounded-full w-4/12 user text-white font-semibold"
        v-on:click="onAccessPage('user')"
      >
        Login Via User
      </button>
      <button
        class="py-1 rounded-full w-4/12 admin text-white font-semibold"
      >
        Login Via Admin
      </button>
    </div>
    <div>
      <admin />
      <users />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import admin  from '../components/admin.vue';
import users from '../components/users.vue'
// import  AdminPage  from './admin/Admin.vue'

export default Vue.extend({
  name: "IndexPage",
  components: {
    // AdminPage
    admin,
    users
  },

  data() {
    return {};
  },

  mounted() {
    // this.getUsersData();
  },

  methods: {
    onAccessPage(access: string) {
      console.log(access)
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
