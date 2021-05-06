<template>
    <div v-if="states.length > 0">
        <h3>You have visited {{ totalVisited }} {{ units }}</h3>
        <p id="all-visited-message" v-if="allAreVisited">You have visited all the states!</p>
    </div>
</template>

<script>
export default {
    name: "StateSummary",
    props: {
        states: Array
    },
    computed: {
        allAreVisited() {
            return this.totalVisited === this.states.length;
        },
        totalVisited() {
            let visitedCount = 0;
            for (let state of this.states) {
                if (state.visited) visitedCount++;
            }
            return visitedCount;
        },
        units() {
            if (this.totalVisited === 1) {
                return "state";
            } else {
                return "states";
            }
        }
    }
}
</script>

<style scoped>

#all-visited-message {
    color: brown;
    font-weight: 600;
}
</style>