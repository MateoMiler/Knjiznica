<template>
  <div id="map" style="height: 100vh; width: 100%;"></div> <!-- Puna visina prikaza za kartu -->
  <q-page padding>
    <!-- sadržaj -->
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue';
import * as L from 'leaflet';
import "leaflet/dist/leaflet.css";

export default {
  setup() {
    const initialMap = ref(null); // Inicijalizacija kao null

    onMounted(() => {
      // Inicijaliziraj kartu s određenom lokacijom i nivoom zumiranja
      initialMap.value = L.map('map').setView([45.3312, 14.4322], 13);

      // Ispravan URL sloja pločica s korištenjem vitičastih zagrada {}
      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      }).addTo(initialMap.value);

      // Dodaj marker na kartu
      const marker = L.marker([45.3312, 14.4322]).addTo(initialMap.value);
      marker.bindPopup('<b>Knjižnica Rijeka</b><br>Ovdje se nalazimo.').openPopup();
    });

    return {
      initialMap
    };
  }
}
</script>

<style scoped>
#map {
    width: 100%;   /* Puna širina */
    height: 100vh; /* Puna visina prikaza */
}
</style>
