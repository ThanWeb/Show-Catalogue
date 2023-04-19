<template>
    <div class="relative show-card">
        <div class="front-side flex flex-col gap-y-4 w-full h-full rounded-3xl overflow-hidden" :class="activeCard !== index && 'active'">
            <div class="grow overflow-hidden">
                <img :src="show.image.original" :alt="show.name" :title="show.name" class="h-full w-full object-cover duration-500">
            </div>
            <div class="flex flex-col gap-y-1 pb-6 px-6">
                <h1>{{ show.name }}</h1>
                <p>{{ show.type }}, {{ show.language }}</p>
                <p>Status: {{ show.status }}</p>
                <a :href="show.url" target="_blank" class="underline hover:text-teal-50 hover:font-semibold">
                    Watch
                </a>
                <button @click="$emit('change-active-card', index)" class="mt-6 rounded-lg hover:text-teal-50 hover:font-semibold">More Info</button>
            </div>
        </div>
        <div class="back-side w-full h-full flex flex-col justify-between p-6 rounded-3xl oveflow-hidden" :class="activeCard === index && 'active'">
            <div class="grow overflow-hidden flex flex-col gap-y-6">
                <div v-if="show.summary" v-html="show.summary" class="h-auto overflow-y-auto"/>
                <p v-else class="h-auto overflow-y-auto">Sorry, there is no summary.</p>
                <p>Genre:
                    <span v-for="(genre, index) in show.genres" :key="index">{{ genre }}{{ index !== show.genres.length - 1 ? ', ' : ''}}</span>
                </p>
                <p>Premiered: {{ show.premiered ? formatDate(show.premiered) : '-' }}</p>
                <p>Ended: {{ show.ended ? formatDate(show.ended) : '-' }}</p>
                <p>Rating:
                    <span v-if="show.rating.average !== null">{{ show.rating.average}} from 10.0</span>
                    <span v-else>Unrated</span>
                </p>
                <p>Network:
                    <a v-if="show.network" :href="show.network.officialSite" target="_blank">
                        <span :class="show.network.officialSite && 'underline'">{{ show.network.name }}</span>, <span>{{ show.network?.country.name }}</span>
                    </a>
                    <span v-else>-</span>
                </p>
                <p>Web Channel:
                    <a v-if="show.webChannel" :href="show.webChannel.officialSite" target="_blank" :class="show.webChannel.officialSite && 'underline'">{{ show?.webChannel?.name || '' }}</a>
                    <span v-else>-</span>
                </p>
            </div>
            <div class="flex flex-col">
                <button @click="$emit('change-active-card', index)" class="mt-6 rounded-lg hover:text-teal-50 hover:font-semibold">Back</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.show-card {
    aspect-ratio: 1 / 2;
}

.show-card ::-webkit-scrollbar {
    height: 0;
}

.show-card:hover img {
    transform: scale(105%);
}

.front-side, .back-side {
    top: 0;
    z-index: -1;
    opacity: 0;
    position: absolute;
    transition: 400ms;
    box-shadow: rgba(52, 211, 253, .4) 0px 2px 8px 0px;
}

.front-side.active, .back-side.active {
    opacity: 1;
    position: static;
}
</style>

<script>
export default {
    props: {
        score: {
            type: Number
        },
        show: {
            type: Object
        },
        activeCard: {
            type: Number
        },
        index: {
            type: Number
        }
    },
    methods: {
        formatDate (string) {
            const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
            return `${string[8] !== '0' ? string[8] : ''}${string[9]} ${months[parseInt(string.slice(5, 7))]} ${string.slice(0, 4)}`
        }
    }
}
</script>
