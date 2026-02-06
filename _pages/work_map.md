---
layout: page
title: work map
permalink: /work-map/
description: An interactive map of places I've worked.
nav: true
nav_order: 7
map: true
---

<style>
  #work-map {
    height: 500px;
    width: 100%;
    border-radius: 8px;
    margin-bottom: 1.5rem;
    z-index: 1;
  }
  .leaflet-div-icon {
    background: transparent;
    border: none;
  }
  .map-icon-marker {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    color: #fff;
    font-size: 18px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.35);
  }
  .leaflet-popup-content h5 {
    margin: 0 0 4px 0;
    font-size: 1rem;
  }
  .leaflet-popup-content p {
    margin: 2px 0;
    font-size: 0.85rem;
  }
  .leaflet-popup-content .popup-title {
    font-weight: 600;
    color: var(--global-theme-color);
  }
  .leaflet-popup-content .popup-years {
    color: #888;
    font-style: italic;
  }
</style>

<div id="work-map"></div>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.min.css" />
<script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.min.js"></script>

<script>
document.addEventListener("DOMContentLoaded", function () {
  // --- JOB DATA ---
  var jobs = [
    {
      company: "Francestown Recreation Department",
      title: "Raft Guard",
      location: "Francestown, NH",
      years: "1994–1995",
      description: "Made sure there was no pushing on the raft!",
      icon: "fa-solid fa-person-swimming",
      color: "#1976d2",
      lat: 42.9876,
      lng: -71.8109
    },
    {
      company: "Blair Bristol Construction",
      title: "Carpenter / Framer / Roofer",
      location: "Antrim, NH",
      years: "1996–2004",
      description: "Built and framed residential homes.",
      icon: "fa-solid fa-house",
      color: "#d84315",
      lat: 43.0281,
      lng: -71.9387
    }
  ];

  // --- MAP INIT ---
  var map = L.map("work-map", {
    scrollWheelZoom: false
  }).setView([43.0, -71.87], 11);

  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    maxZoom: 18
  }).addTo(map);

  // --- ADD MARKERS ---
  var bounds = [];
  jobs.forEach(function (job) {
    var iconHtml =
      '<div class="map-icon-marker" style="background:' + job.color + ';">' +
        '<i class="' + job.icon + '"></i>' +
      '</div>';

    var marker = L.marker([job.lat, job.lng], {
      icon: L.divIcon({
        className: "leaflet-div-icon",
        html: iconHtml,
        iconSize: [40, 40],
        iconAnchor: [20, 20],
        popupAnchor: [0, -20]
      })
    }).addTo(map);

    marker.bindPopup(
      '<h5 class="popup-title">' + job.company + '</h5>' +
      '<p><strong>' + job.title + '</strong></p>' +
      '<p class="popup-years">' + job.location + ' · ' + job.years + '</p>' +
      '<p>' + job.description + '</p>'
    );

    bounds.push([job.lat, job.lng]);
  });

  // fit map to markers with padding
  if (bounds.length > 1) {
    map.fitBounds(bounds, { padding: [50, 50] });
  }
});
</script>
