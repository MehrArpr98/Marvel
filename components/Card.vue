<template>

    <nuxt-link v-if="itemExist" :to="{ name: 'about', params: { id: item.id } }">
        <div
            class="rounded-lg h-full flex flex-col gap-3 p-3 border border-[var(--base-background)] hover:border-[var(--base-gray-3)] hover:[&>img]:scale-[1.03] duration-300">
            <img :src="`${item.thumbnail.path}.${item.thumbnail.extension}`" alt="marvel-character-img"
                class="rounded-md duration-300 w-full grow" />
            <span class="text-white">{{ item.name }}</span>
        </div>
    </nuxt-link>
    <div v-else class="rounded-lg h-full flex flex-col gap-3 p-3 border border-[var(--base-background)] duration-300">
        <span
            class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] w-full h-72 rounded-md w-full grow"></span>
        <span class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] w-1/2 h-5"></span>
    </div>
</template>
<script>

export default {
    name: "Card",
    props: {
        item: {
            type: Object,
            required: true,
            default: () => ({})
        },
    },
    computed: {
        itemExist() {
            return Object.keys(this.item).length;
        },

    },

}

</script>
<style>
.skeleton-box::after {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    transform: translateX(-100%);
    background-image: linear-gradient(90deg, rgba(255, 255, 255, 0) 0, rgba(255, 255, 255, 0.2) 20%, rgba(58, 48, 48, 0.5) 60%, rgba(255, 255, 255, 0));
    animation: shimmer 1s infinite;
    content: '';
}

@keyframes shimmer {
    100% {
        transform: translateX(100%);
    }
}
</style>