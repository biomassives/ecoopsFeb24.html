/* global L */

<template>
  <div id="map" class="map-container"></div>
</template>

<script>
import L from 'leaflet';
import 'leaflet-draw';

export default {
  name: 'MapComponent',
  mounted() {

    const map = L.map('map').setView([51.505, -0.09], 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors'
    }).addTo(map);

    this.map.addLayer(this.drawnItems);

    const drawControl = new L.Control.Draw({
      edit: {
          featureGroup: this.drawnItems
      }
    });




  this.map.addControl(drawControl);

    this.map.on(L.Draw.Event.CREATED, (event) => {
    const layer = event.layer;
    const content = `<form><input type="text" id="feature-label" placeholder="Enter label"/><button type="submit">Save</button></form>`;
    layer.bindPopup(content, { closeOnClick: false, closeButton: false }).openPopup();
    layer.on('popupopen', () => {
      document.getElementById('feature-label').focus();
      document.querySelector('form').onsubmit = (e) => {
        e.preventDefault();
        const label = document.getElementById('feature-label').value;
        this.labels[layer._leaflet_id] = label;
        layer.bindPopup(label); // Update popup with label
        layer.closePopup();
      };
    });
    this.drawnItems.addLayer(layer);
  });

    // Geolocation functionality to zoom into the user's location
    navigator.geolocation.getCurrentPosition((position) => {
      const { latitude, longitude } = position.coords;
      map.setView([latitude, longitude], 14);
      L.marker([latitude, longitude]).addTo(map).bindPopup('You are here!').openPopup();
    }, () => {
      console.log('Geolocation not available or permission denied.');
    });

    // Leaflet Draw Plugin Initialization for drawing tools
    const drawnItems = new L.FeatureGroup().addTo(map);
    new L.Control.Draw({
      edit: {
        featureGroup: drawnItems,
        poly: {
          allowIntersection: false
        }
      },
      draw: {
        polygon: {
          allowIntersection: false,
          showArea: true
        },
        polyline: {},
        rect: {},
        circle: false,
        marker: true
      }
    }).addTo(map);

    // Handling created draw elements
    map.on(L.Draw.Event.CREATED, (event) => {
      const layer = event.layer;
      drawnItems.addLayer(layer);
      // You can also add event listeners to the layer here if needed



    });
  }
}
</script>

<style scoped>
.map-container {
  height: 400px;
}
.leaflet-attribution-flag {
 display:none;
}

</style>

