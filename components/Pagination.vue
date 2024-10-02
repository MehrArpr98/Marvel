<template>
    <div class="flex justify-center w-full">
        <ul v-if="total_pages > 1" class="flex pl-0 list-none rounded my-2">
            <li :class="{ 'hover:bg-gray-400': !isInFirstPage }">
                <button type="button" :class="{ 'cursor-not-allowed': isInFirstPage }" :disabled="isInFirstPage"
                    @click="gotoFirst">
                    &laquo;
                </button>
            </li>

            <li :class="{ 'hover:bg-gray-400': !isInFirstPage }">
                <button type="button" :class="{ 'cursor-not-allowed': isInFirstPage }" :disabled="isInFirstPage"
                    @click="gotoPrevious">
                    &lsaquo;
                </button>
            </li>

            <template v-if="showDots('left')">
                <li class=" hover:bg-gray-400" :class="{ 'bg-gray-600': isInFirstPage }">
                    <button type="button" :class="{ 'cursor-not-allowed': isInFirstPage }" :disabled="isInFirstPage"
                        @click="gotoPageNumber(1)">
                        1
                    </button>
                </li>

                <li>
                    <button type="button" :disabled="true">
                        ...
                    </button>
                </li>
            </template>

            <li class=" hover:bg-gray-400" v-for="(page, index) in pages" :key="`pages_${index}`"
                :class="{ 'bg-[var(--base-red)]': page === currentPage }">
                <button type="button" :class="{ 'cursor-not-allowed': page === currentPage }"
                    :disabled="page === currentPage" @click="gotoPageNumber(page)">
                    {{ page }}
                </button>
            </li>

            <template v-if="showDots('right')">
                <li>
                    <button type="button" :disabled="true">
                        ...
                    </button>
                </li>

                <li class=" hover:bg-gray-400" :class="{ 'bg-gray-600': isInLastPage }">
                    <button type="button" :class="{ 'cursor-not-allowed': isInLastPage }" :disabled="isInLastPage"
                        @click="gotoPageNumber(total_pages)">
                        {{ total_pages }}
                    </button>
                </li>
            </template>

            <li :class="{ 'hover:bg-gray-400': !isInLastPage }">
                <button type="button" :class="{ 'cursor-not-allowed': isInLastPage }" :disabled="isInLastPage"
                    @click="gotoNext">
                    &rsaquo;
                </button>
            </li>

            <li :class="{ 'hover:bg-gray-400': !isInLastPage }">
                <button type="button" :class="{ 'cursor-not-allowed': isInLastPage }" :disabled="isInLastPage"
                    @click="gotoLast">
                    &raquo;
                </button>
            </li>
        </ul>
    </div>
</template>

<script>

export default {

    name: "Pagination",
    template: '#pagination',
    props: {
        currentPage: {
            type: Number,
            required: true,
            default: 1
        },
        pagination: {
            type: Object,
            required: true,
            default: () => ({})
        },
        maxVisibleButtons: {
            type: Number,
            required: false,
            default: 5
        }
    },
    data: () => ({
        per_page: 10,
        total: 0,
        total_pages: 0
    }),
    watch: {
        pagination: {
            handler(pagination) {
                this.per_page = pagination.per_page || 10;
                this.total = pagination.total || 0;
                this.total_pages = pagination.total_pages || 0;
            },
            immediate: true
        }
    },
    computed: {
        isInFirstPage() {
            return this.currentPage === 1;
        },
        isInLastPage() {
            return this.currentPage === this.total_pages;
        },
        pages() {
            const range = [];
            for (let i = this.startPage; i <= this.endPage; i += 1) {
                range.push(i);
            }
            return range;
        },
        startPage() {
            if (this.currentPage === 1) {
                return 1;
            }
            if (this.currentPage === this.total_pages) {
                return this.total_pages - this.maxVisibleButtons + 1;
            }
            return this.currentPage - 1;
        },
        endPage() {
            return Math.min(this.startPage + this.maxVisibleButtons - 1, this.total_pages);
        }
    },
    methods: {
        showDots(position = "left") {
            const number = position === "left" ? 1 : this.total_pages;
            const nextNumber = position === "left" ? 2 : this.total_pages - 1;
            return !this.pages.includes(number) || !this.pages.includes(nextNumber);
        },
        gotoFirst() {
            this.gotoPageNumber(1);
        },
        gotoLast() {
            this.gotoPageNumber(this.total_pages);
        },
        gotoPrevious() {
            this.gotoPageNumber(this.currentPage - 1);
        },
        gotoNext() {
            this.gotoPageNumber(this.currentPage + 1);
        },
        gotoPageNumber(pageNumber) {
            this.$emit("page_changed", pageNumber);
        }
    }

}


</script>
<style>
ul {
    list-style: none;
    gap: 0.5rem;
}

ul li {
    cursor: pointer;
    width: 24px;
    height: 24px;
    text-align: center;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    color: white
}
</style>