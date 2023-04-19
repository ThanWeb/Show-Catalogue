<script setup>
import ShowCard from './components/ShowCard.vue'
</script>

<template>
    <div class="container grid gap-6 lg:gap-8 sm:grid-cols-2 lg:grid-cols-4 px-6 py-6 sm:py-10 lg:py-16 mx-auto">
        <ShowCard v-for="(item, index) in shows" v-bind="item" :key="index" :index="index" @change-active-card="changeActiveCard(index)" :active-card="activeCard"/>
    </div>
</template>

<script>
export default {
    data () {
        return {
            shows: [],
            activeCard: -1
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
        },
        changeActiveCard (index) {
            if (this.activeCard === index) {
                this.activeCard = -1
            } else {
                this.activeCard = index
            }
        }
    }
}
</script>
