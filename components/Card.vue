<template>
    <SkeletonCard v-if="!itemExist" />
    <nuxt-link v-else :to="item?.id ?{ name: 'details-id', params: { id: item?.id }}: { name: 'details-id', params: { id: $route.params?.id }}">
        <div
            class="rounded-lg h-full flex flex-col gap-3 p-3 border border-[var(--base-background)] hover:border-[var(--base-gray-3)] hover:[&>img]:scale-[1.03] duration-300">
            <img :src="`${item.thumbnail.path}.${item.thumbnail.extension}`" alt="marvel-character-img"
                class="rounded-md duration-300 w-full grow" />
            <span class="text-white line-clamp-1">{{ item.name }}</span>
        </div>
    </nuxt-link>
    
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