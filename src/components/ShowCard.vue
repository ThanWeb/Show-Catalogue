<template>
    <div>
        <img
            :src="show.image.original"
            :alt="show.name"
            :title="show.name"
            class="w-full"
        >
        <h1 class="text-red-700">{{ show.name }}</h1>
    </div>
</template>

<script>
export default {
    props: {
        score: {
            type: Number
        },
        show: {
            type: Object
        }
    }
}
</script>
