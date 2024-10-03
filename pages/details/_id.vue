<template>
    <div class="min-h-screen flex flex-col">
        <div class="header ">
            <div class="container mx-auto flex flex-col gap-4 md:gap-8 py-3 md:py-4 px-3 md:px-0 relative">
                <img src="~/static/logo.png" alt="logo-img" class="w-24" />
                <img src="~/static/redShadow.svg" class="absolute w-1/2 h-full md:w-[200px] md:h-[150px] left-0 md:left-[300px] top-[100px] scale-[2] md:scale-[4]"/>
                <div class="relative flex flex-col md:flex-row gap-4 my-5">
                    <SkeletonInfo v-if="!itemExist" />
                    <template v-else> <img :src="`${item.thumbnail.path}.${item.thumbnail.extension}`"
                            alt="marvel-character-img" class="rounded-md duration-300 w-[180px] h-[180px] md:h-60 md:w-60" />

                        <div class="flex flex-col gap-3 grow p-0 md:p-6">
                            <h1 class="text-white text-[32px] leading-[50px]">{{ item.name }}</h1>
                            <div class="text-[var(--base-gray-5)] text-xs	">
                                {{ item.description }}
                            </div>
                            <div class="flex gap-2">
                                <a v-for="url in item.urls" :href="url.url" target="_blank"
                                    class="border border-[var(--base-gray-4)] rounded px-3 py-1 text-white rounded">{{
                                        url.type }}
                                </a>
                            </div>
                        </div>
                    </template>

                </div>
            </div>
        </div>
        <div class="bg-[var(--base-background)] grow flex flex-col justify-between gap-10 py-10 z-10">
            <div class="container mx-auto flex flex-col gap-12">
                <div class="flex flex-col gap-6 px-3 md:px-0">
                    <h1 class="text-white text-2xl">Comics</h1>
                    <div class="w-full grid grid-cols-1 md:grid-cols-4 gap-4 auto-rows-fr ">
                        <Card v-for="item in comics" :item="item" />

                    </div>
                </div>

                <div class="flex flex-col gap-6 px-3 md:px-0">
                    <h1 class="text-white text-2xl">Series</h1>
                    <div class="w-full grid grid-cols-1 md:grid-cols-4 gap-4 auto-rows-fr ">
                        <Card v-for="item in series" :item="item" />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
import 'static/index.css'

export default {
    name: 'Details',
    data() {
        return {
            currentPage: 1,
            item: [],
            comics: [],
            series: []
        };
    },
    methods: {
        onPageChange(page) {
            this.currentPage = page;
            this.getCharacterInfo()
        },
        setComicsAndSeries({ comics, series }) {
            this.comics = []
            this.series = []
            comics.forEach((item) => {
                axios.get(`${item.resourceURI}?ts=1&apikey=8d7d487301527f87f231c81d4e007304&hash=863c39e9e0dc00aad089dc5ff2d9724a`).then(response => {
                    this.comics.push({ thumbnail: response.data.data.results[0].thumbnail,  name: item.name })
                })
            })
            series.forEach((item) => {
                axios.get(`${item.resourceURI}?ts=1&apikey=8d7d487301527f87f231c81d4e007304&hash=863c39e9e0dc00aad089dc5ff2d9724a`).then(response => {
                    this.series.push({ thumbnail: response.data.data.results[0].thumbnail,  name: item.name })
                })
            })
        },
        getCharacterInfo() {
            this.comics = new Array(4)
            this.series = new Array(4)

            let url = 'https://gateway.marvel.com:443/v1/public/characters'
            axios.get(`${url}/${this.characterId}?ts=1&apikey=8d7d487301527f87f231c81d4e007304&hash=863c39e9e0dc00aad089dc5ff2d9724a`).then(response => {
                this.item = response.data.data.results[0];
                this.setComicsAndSeries({ comics: response.data.data.results[0].comics?.items, series: response.data.data.results[0].series?.items })
            })

        }
    },
    mounted: function () {
        this.getCharacterInfo()
    },
    computed: {
        characterId() {
            return this.$route.params.id
        },
        itemExist() {
            return Object.keys(this.item).length;
        },
    },


}


</script>