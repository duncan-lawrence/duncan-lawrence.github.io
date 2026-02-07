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
  // --- JITTER: offset coordinates by ~5-10 miles for privacy ---
  function jitter(coord) {
    var offset = (Math.random() - 0.5) * 0.07; // ~2-5 mile random offset
    return coord + offset;
  }

  // --- JOB DATA (coordinates are approximate, jittered for privacy) ---
  var jobs = [
    {
      company: "Francestown Recreation Department",
      title: "Raft Guard",
      years: "1994–1995",
      description: "Made sure there was no pushing on the raft!",
      icon: "fa-solid fa-person-swimming",
      color: "#1976d2",
      lat: jitter(42.99), lng: jitter(-71.81)
    },
    {
      company: "Lawrence's Lawns",
      title: "Head Mower",
      years: "1995",
      description: "Ran my own lawn mowing business. Had to be within walking distance!",
      icon: "fa-solid fa-seedling",
      color: "#388e3c",
      lat: jitter(42.99), lng: jitter(-71.81)
    },
    {
      company: "Blair Bristol Construction",
      title: "Carpenter / Framer / Roofer",
      years: "1996–2004",
      description: "Built and framed residential homes.",
      icon: "fa-solid fa-house",
      color: "#d84315",
      lat: jitter(43.03), lng: jitter(-71.94)
    },
    {
      company: "Hamilton College Outdoor Leadership",
      title: "Facilitator",
      years: "2001–2004",
      description: "Climbed trees and expanded minds through challenge by choice.",
      icon: "fa-solid fa-tree",
      color: "#2e7d32",
      lat: jitter(43.05), lng: jitter(-75.40)
    },
    {
      company: "Hulbert Outdoor Center",
      title: "Instructor",
      years: "2004",
      description: "Led groups through week long experiential education journeys.",
      icon: "fa-solid fa-tree",
      color: "#2e7d32",
      lat: jitter(43.90), lng: jitter(-72.16)
    },
    {
      company: "Wilderness Adventures",
      title: "Wilderness Guide / Trip Director",
      years: "2004",
      description: "Led multi-week wilderness trips.",
      icon: "fa-solid fa-hiking",
      color: "#5d4037",
      lat: jitter(43.74), lng: jitter(-110.80)
    },
    {
      company: "Jackson Hole Mtn Resort",
      title: "Rental Tech",
      years: "2004–2005",
      description: "Made sure your boots and skis fit perfectly.",
      icon: "fa-solid fa-skiing",
      color: "#0288d1",
      lat: jitter(43.59), lng: jitter(-110.83)
    },
    {
      company: "Best Western",
      title: "Bell Hop",
      years: "2004–2005",
      description: "Getting your bag to your room was my mission.",
      icon: "fa-solid fa-concierge-bell",
      color: "#7b1fa2",
      lat: jitter(43.59), lng: jitter(-110.82)
    },
    {
      company: "US State Department",
      title: "Fulbright ETA",
      years: "2005",
      description: "Taught English at a teacher training college.",
      icon: "fa-solid fa-book",
      color: "#1565c0",
      lat: jitter(-33.08), lng: jitter(-68.47)
    },
    {
      company: "Wilderness Adventures",
      title: "Wilderness Guide / Trip Director",
      years: "2006",
      description: "Led multi-week adventure trips.",
      icon: "fa-solid fa-hiking",
      color: "#5d4037",
      lat: jitter(-0.18), lng: jitter(-78.47)
    },
    {
      company: "Wilderness Adventures",
      title: "Wilderness Guide / Trip Director",
      years: "2006",
      description: "Led multi-week adventure trips.",
      icon: "fa-solid fa-hiking",
      color: "#5d4037",
      lat: jitter(8.53), lng: jitter(-83.53)
    },
    {
      company: "Wilderness Adventures",
      title: "Wilderness Guide / Trip Director",
      years: "2006",
      description: "Led multi-day family adventure trips.",
      icon: "fa-solid fa-hiking",
      color: "#5d4037",
      lat: jitter(44.46), lng: jitter(-110.83)
    },
    {
      company: "Teton Youth and Family Services",
      title: "Youth Counselor",
      years: "2006–2007",
      description: "Mentored and ensured the safety of up to 9 children in a youth shelter.",
      icon: "fa-solid fa-handshake",
      color: "#e65100",
      lat: jitter(43.48), lng: jitter(-110.76)
    },
    {
      company: "El Puente",
      title: "Medical Interpreter and Health Navigator",
      years: "2006–2007, 2010",
      description: "Helped Spanish-speaking patients navigate the health system.",
      icon: "fa-solid fa-kit-medical",
      color: "#c62828",
      lat: jitter(43.48), lng: jitter(-110.76)
    },
    {
      company: "University of Colorado Boulder",
      title: "Graduate Instructor",
      years: "2007–2013",
      description: "Taught undergrads comparative politics, IPE, and development.",
      icon: "fa-solid fa-book",
      color: "#1565c0",
      lat: jitter(40.01), lng: jitter(-105.27)
    },
    {
      company: "University of Colorado Boulder",
      title: "Methods Mentor",
      years: "2012",
      description: "Provided survey design and implementation expertise.",
      icon: "fa-solid fa-magnifying-glass",
      color: "#4527a0",
      lat: jitter(-16.41), lng: jitter(-71.54)
    },
    {
      company: "Telluride Research Group",
      title: "Co-founder",
      years: "2012–2016",
      description: "Co-founded and led a data analysis and research firm.",
      icon: "fa-solid fa-chart-line",
      color: "#00838f",
      lat: jitter(40.01), lng: jitter(-105.27)
    },
    {
      company: "US State Department",
      title: "Fulbright Scholar",
      years: "2013",
      description: "Led research on immigration attitudes.",
      icon: "fa-solid fa-book",
      color: "#1565c0",
      lat: jitter(-33.45), lng: jitter(-70.66)
    },
    {
      company: "Rocky Mountain Institute",
      title: "Associate",
      years: "2013–2014",
      description: "Consulted and designed new programs.",
      icon: "fa-solid fa-pen",
      color: "#37474f",
      lat: jitter(40.01), lng: jitter(-105.27)
    },
    {
      company: "Stanford University",
      title: "Executive Director",
      years: "2014–2022, 2025–Present",
      description: "Co-founded and led the Immigration Policy Lab.",
      icon: "fa-solid fa-book",
      color: "#1565c0",
      lat: jitter(37.43), lng: jitter(-122.17)
    },
    {
      company: "Welcome.us",
      title: "Consultant",
      years: "2022",
      description: "Guided data strategy.",
      icon: "fa-solid fa-chart-line",
      color: "#00838f",
      lat: jitter(45.52), lng: jitter(-122.68)
    },
    {
      company: "International Rescue Committee",
      title: "Senior Director of Innovation",
      years: "2023–2025",
      description: "Led innovation in US and Europe.",
      icon: "fa-solid fa-handshake",
      color: "#e65100",
      lat: jitter(45.52), lng: jitter(-122.68)
    }
  ];

  // --- MAP INIT ---
  var map = L.map("work-map", {
    scrollWheelZoom: false
  }).setView([20, -90], 3);

  L.tileLayer("https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png", {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> &copy; <a href="https://carto.com/">CARTO</a>',
    maxZoom: 12
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
      '<p class="popup-years">' + job.years + '</p>' +
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
