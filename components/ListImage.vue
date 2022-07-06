<template>
<div class="w-full">
    <div class="grid grid-cols-2 gap-8 w-full" v-if="listImage.length !== 0">
        <div v-for="img in listImage" :key="img.id" class="flex space-x-2 border-1 shadow-lg rounded-md bg-white p-4 w-full">
            <img :src="img.url" alt="" width="200px" height="200px">
            <div class="flex flex-col space-y-4">
                <p class="text-xl capitalize">
                    Album {{ img.albumId }}
                </p>
                <div class="flex space-x-2">
                    <button class="text-center px-4 py-2 rounded-md text-white bg-yellow-400 text-nowrap">
                        Ubah Nama Gambar
                    </button>
                    <button class="text-center px-4 py-2 rounded-md text-white bg-red-500 text-nowrap">
                        Hapus Gambar
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
    title: string,
    url: string,
    albumId: number
}
import Vue from 'vue';
// import VueTailwindPagination from '@ocrv/vue-tailwind-pagination'
import { PropType } from 'vue/types/v3-component-props';
export default Vue.extend({
    props: { listImage: {
        type: Array as PropType<ImageInterface[]>
    } },
    data() {
        return {
            page: 10,
        }
    },
    methods: {
        getImageSource(url: string) {
            return require(`../${url}`);
        }
    },
    components: {
    }

})
</script>

<style lang="css">
.text-nowrap {
    white-space: nowrap;
}
</style>