<template>
    <div class="map-container">
        <div id="map"></div>
        <button @click="saveMarkers">Save Markers</button>
        <!--Add clear button-->
    </div>
</template>

<script>
import L from "leaflet";
import "leaflet/dist/leaflet.css";

const customIcon = L.icon({
    iconUrl: "/marker-icon.png",
    iconSize: [30, 30],
    iconAnchor: [15, 30]
});

export default {
    data() {
        return {
            map: null,
            markers: [],
        };
    },
    mounted() {
        this.initMap();
        this.loadMarkers();
    },
    methods: {
        initMap() {
            this.map = L.map("map").setView([38.8283, -98.5795], 4); // geographic center of the US
            L.tileLayer("https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png").addTo(this.map);

            this.map.on("click", this.onMapClick);
        },
        onMapClick(event) {
            const latlng = event.latlng;
            const markerData = { lat: latlng.lat, lng: latlng.lng };
            this.markers.push(markerData); // Store marker data, not L.Marker objects

            L.marker(latlng, { icon: customIcon }).addTo(this.map); // Add marker to map display
        },
        saveMarkers() {
            localStorage.setItem("markers", JSON.stringify(this.markers)); // saves to the broswer locally
        },
        loadMarkers() {
            const savedMarkers = localStorage.getItem("markers");
            console.log(savedMarkers);
            if (savedMarkers) {
                this.markers = JSON.parse(savedMarkers);

                this.markers.forEach((markerData) => {
                    const latlng = L.latLng(markerData.lat, markerData.lng);
                    L.marker(latlng, { icon: customIcon }).addTo(this.map);
                });
            }
        },
    },
}
</script>

<style>
.map-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
}
#map {
    width: 80%;
    height: 600px;
    margin-bottom: 10px;
}
</style>