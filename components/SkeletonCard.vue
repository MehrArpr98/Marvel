<template>
    <div class="rounded-lg h-full flex flex-col gap-3 p-3 border border-[var(--base-background)] duration-300">
        <span
            class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] w-full h-72 rounded-md w-full grow"></span>
        <span class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] w-1/2 h-5"></span>
    </div>
</template>
<script>

export default {
    name: "SkeletonCard",
}