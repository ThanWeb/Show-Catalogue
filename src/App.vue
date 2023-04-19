<script setup>
import ShowCard from './components/ShowCard.vue'
</script>

<template>
    <div>
        <ShowCard v-for="(item, index) in shows" v-bind="item" :key="index"/>
        <h1 class="text-red-700">a</h1>
    </div>
</template>

<script>
export default {
    data () {
        return {
            shows: []
        }
    },
    mounted () {
        this.getShows()
    },
    methods: {
        async getShows () {
            const response = await fetch('http://api.tvmaze.com/search/shows?q=girls')
            const responseJson = await response.json()
            this.shows = responseJson
        }
    }
}
</script>
