<template>
  <div class="min-h-screen flex flex-col">
    <div class="header ">
      <div class="container mx-auto flex flex-col gap-4 md:gap-8 py-3 md:py-4 px-3 md:px-0">
        <img src="~/static/logo.png" alt="logo-img" class="w-24 z-10" />
        <img src="~/static/redShadow.svg" class="absolute w-1/2 md:w-[200px] h-[150px] left-0 md:left-[300px] scale-[2] md:scale-[4]"/>
        <div class="relative">
           
          <div class="w-full flex gap-4 bg-[var(--base-background)] p-4 z-10 rounded-lg">
            <input type="text" placeholder="Search for characters..." v-model="searchText"
              class="grow px-3 py-2 rounded bg-[var(--base-gray-2)] text-gray-100 outline-none focus:border-[var(--base-gray-3)]">
            <button class="bg-red-500 p-2 text-white rounded" @click="getCharacters">&#x1F50E;&#xFE0E; <span
                class="hidden md:contents">search</span></button>
          </div>
        </div>
      </div>
    </div>
    <div class="bg-[var(--base-background)] grow flex flex-col justify-between gap-10 py-10 z-10">
      <div class="w-full grid grid-cols-1 md:grid-cols-4 gap-4 auto-rows-fr container mx-auto px-3 md:px-0">
        <Card v-for="item in items" :key="item?.id" :item="item" />
      </div>

      <Pagination :pagination="{
        per_page: perPage,
        total: total,
        total_pages: Math.ceil(total / perPage)
      }" :current-page="currentPage" @page_changed="onPageChange" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import '../static/index.css'

export default {
  name: 'IndexPage',
  data() {
    return {
      currentPage: 1,
      total: 0,
      searchText: '',
      items: []
    };
  },
  methods: {
    onPageChange(page) {
      this.currentPage = page;
      this.getCharacters()
    },
    getCharacters() {
      this.items = new Array(this.perPage)
      let url = 'https://gateway.marvel.com:443/v1/public/characters?'
      if (this.searchText)
        url += `nameStartsWith=${this.searchText}&`
      axios.get(`${url}limit=${this.perPage}&offset=${this.perPage * this.currentPage}&ts=1&apikey=8d7d487301527f87f231c81d4e007304&hash=863c39e9e0dc00aad089dc5ff2d9724a`).then(response => {
        this.items = response.data.data.results;
        this.total = response.data.data.total;
      })

    }
  },
  mounted: function () {
    this.getCharacters()
  },
  computed: {
    isInFirstPage() {
      return this.currentPage === 1;
    },
    perPage() {
      return this.$store.state.per_page
    }
  },
}

</script>

