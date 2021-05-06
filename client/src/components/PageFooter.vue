<template>
    <div class="footer">
        
        <div class="m-2">
            <span class="p-3">
                <router-link to="/">Home</router-link>
            </span>

            <span class="p-3">
                <router-link to="/about">About this site</router-link>
            </span>
        </div>

        <p>Header image by
            <a href="https://unsplash.com/photos/KpBXAOs80YI">@chrislawton on Unsplash</a>
        </p>
        <p>
            <a target="_blank" href="https://icons8.com/icon/43632/map">Map Icon</a> by <a target="_blank" href="https://icons8.com/">Icons8</a>
        </p>
    </div>
</template>

<script>
export default {
    name: "PageFooter",
}
</script>

<style scoped>
span {
    display: inline;
    margin-right: 0.5em;
}
</style>