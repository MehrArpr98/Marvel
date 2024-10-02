<template>
    <main class="relative flex flex-col md:flex-row gap-4 my-5">
        <span
            class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] rounded-md mb-3 md:h-60 md:w-60"></span>
        <div class="flex flex-col gap-3 grow p-3 md:p-6">
            <span class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] h-10 w-28"></span>
            <span class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] h-3 w-1/2"></span>
            <span class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] h-3 w-1/3 ">
            </span>
            <div class="flex gap-2 mt-4">
                <span v-for="i in 3"
                    class="skeleton-box inline-block relative overflow-hidden bg-[var(--base-gray-3)] rounded h-5 w-10">
                </span>
            </div>
        </div>
    </main>
</template>
<script>

export default {
    name: "SkeletonInfo",
}