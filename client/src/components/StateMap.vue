<template>
    <div class="state-map">
        <h2>The state of {{ state.name }}</h2>

        <p v-if="state.visited">You have visited this state</p>
        <p v-else>You have not visited this state</p>

        <div id="map-container" v-if="dataReady">
            <l-map ref="map" v-on:ready="onMapReady" v-bind:zoom="state.zoom" v-bind:center="mapCenter">
                <l-tile-layer
                url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
                attribution="&copy; OpenStreetMap contributors">
                </l-tile-layer>
            </l-map>
        </div>
    </div>
</template>

<script>

import { LMap, LTileLayer } from '@vue-leaflet/vue-leaflet'

export default {
    name: "StateMap",
    components: { LMap, LTileLayer },
    data() {
        return {
            state: {},
            dataReady: false,
            mapReady: false
        }
    },
    mounted() {
        this.state.name = this.$route.params.state 
        this.fetchStateData()
    },
    methods: {
        onMapReady() {
            this.mapReady = true;
            this.setMapView();
        },
        setMapView() {
          if(this.dataReady && this.mapReady) {
              this.$refs.map.leafletObject.setView(this.mapCenter, this.state.zoom);
          }  
        },
        fetchStateData() {
            this.$stateService.getOneState(this.state.name).then( state => {    
                this.state = state;
                this.dataReady = true;
                this.setMapView();
            })
            .catch( err => {
                if (err.response && err.response.status === 404) {
                    this.state.name = "?";
                } else {
                    alert("Sorry, error fetching data about this state.");
                    console.log(err);
                }
            });
        }
    },
    computed: {
        mapCenter() {
            return [this.state.lat, this.state.lon];
        }
    }
}
</script>

<style scoped>
#map-container {
    height: 30em;
}
</style>