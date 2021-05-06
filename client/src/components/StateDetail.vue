<template>
    <div class="state-info">
        <span class="state-name">{{ state.name }}</span>
        <div>
            <input class="visit-state" type="checkbox" v-model="visited">
        </div>
        <router-link v-bind:to="{ name: 'StateMap', params: { state: state.name}}">
            <img class="map-icon" src="@/assets/map_icon.png">
        </router-link>
    </div>
</template>

<script>
export default {
    name:"StateDetail",
    emits: ["update-visited"],
    props: {
        state: Object
    },
    data() {
        return {
            visited: this.state.visited
        }
    },
    watch: {
        visited() {
            this.$emit("update-visited", this.state.name, this.visited);
        }
    }
}
</script>

<style scoped>

.state-info {
    padding: 1rem;
    height: 8rem;
    width: 10rem;
    border: 1px gainsboro solid;
    border-radius: .3rem;
    background-color: whitesmoke;
}

.visit-state {
    margin: 1rem;
}

.map-icon {
    width: 3rem;
    height: 3rem;
}
</style>