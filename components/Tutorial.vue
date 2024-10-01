<template>
  <div class="">
    <div class="header ">
      <div class="container mx-auto flex flex-col gap-4 py-5 px-2 md:px-0">
        <img src="http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available.jpg" alt="logo-img"
          class="w-10 h-5" />
        <div class="relative">
          <!--  <div class="red-shadow absolute w-52 h-36 left-28 top-4 z-0"></div> -->
          <div class="w-full flex gap-4 bg-[var(--base-background)] p-4 z-10 rounded-lg">
            <input type="text" placeholder="Search for characters..."
              class="grow px-3 py-2 rounded bg-[var(--base-gray-2)] outline-none focus:border-[var(--base-gray-3)]">
            <button class="bg-red-500 p-2 text-white rounded">search</button>
          </div>
        </div>
      </div>
    </div>


    <div class="bg-[var(--base-background)] ">
      <div class="w-full grid grid-cols-1 md:grid-cols-4 gap-8 container mx-auto py-10 px-2 md:px-0">
        <template v-for="i in 50">
          <nuxt-link :to="{ name: 'about', params: { id: 123 } }">
            <div
              class="rounded-lg p-3 border border-[var(--base-background)] hover:border-[var(--base-gray-3)] duration-300">
              <img src="http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available.jpg" alt="marvel-character-img"
                class="rounded-md" />
              <span class="text-white">title</span>


            </div>


          </nuxt-link>
        </template>


      </div>


      <Pagination :pagination="{
        per_page: 10,
        total: 187,
        total_pages: 19
      }" :current-page="currentPage" @pagechanged="onPageChange" />
    </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'NuxtTutorial',
  data() {
    return {
      currentPage: 1,
    };
  },
  methods: {
    onPageChange(page) {
      this.currentPage = page;
    }
  },

}


</script>
<style>
body {
  --base-red: #DC2626;
  --base-background: #2C2E30;
  --base-gray-2: #3B3D3F;
  --base-gray-3: #404244;

}

.header {
  background: linear-gradient(90deg, #2C2E30 -0.76%, #0E0E0E 50%);


}

.red-shadow {
  /*  background: #DC262652; */
  /*  backdrop-filter: blur(160px) */
  /*  backdrop-filter: #DC262652 blur(160px) saturate(150%); */
  background: rgba(220, 38, 38, 0.32);
  backdrop-filter: blur(160px);
}
</style>
