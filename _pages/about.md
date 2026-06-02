---
permalink: /
title: "About Me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I received the B.S. degree in Applied Physics from [Beijing Institute of Technology](https://english.bit.edu.cn/), Beijing China in 2020. Then I obtained the M.Phil. degree in Computer and Information Engineering from [The Chinese University of Hong Kong (Shenzhen)](https://www.cuhk.edu.cn/en), in 2022 under the supervision of [Prof. Kaiming SHEN](https://kaimingshen.github.io/index.html).

Currently, I'm working toward the Ph.D. in Physics at [The Hong Kong University of Scicence and Technology](https://hkust.edu.hk/) supervised by [Prof. Ding PAN](https://facultyprofiles.hkust.edu.hk/profiles.php?profile=ding-pan-dingpan). 

## Research Interests
My research interests encompass Optimization, Statistics, and Computational Physics. Recently, I have been investigating generative AI, with a particular focus on explicit probabilistic models such as normalizing flows.

## Update

**Mar. 28, 2026**: I am expected to graduate in 2027 spring. I am looking for postdoctoral opportunities in *AI4Science* and *Molecular Dynamics Simulations*. If you are interested in my profile, please feel free to drop me an email.











## Visitors
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<div id="visitor-map" style="height: 350px; width: 100%; margin: 0 auto; border-radius: 8px; overflow: hidden;"></div>
<p style="text-align: center; font-size: 0.8em; color: #888;" id="visitor-count"></p>
<script>
(function() {
  var WORKER_URL = "https://visitor-map.bitzhangyaowen.workers.dev";

  fetch(WORKER_URL + "/visit", { method: "POST" }).catch(function(){});

  fetch(WORKER_URL + "/visitors")
    .then(function(r) { return r.json(); })
    .then(function(visitors) {
      document.getElementById("visitor-count").textContent = "Total visits: " + visitors.length;

      var map = L.map("visitor-map").setView([20, 0], 2);
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution: "&copy; OpenStreetMap contributors",
        maxZoom: 18,
      }).addTo(map);

      var markers = L.markerClusterGroup
        ? L.markerClusterGroup()
        : L.layerGroup();

      visitors.forEach(function(v) {
        if (v.lat && v.lon) {
          var m = L.marker([parseFloat(v.lat), parseFloat(v.lon)]);
          m.bindPopup("<b>" + (v.city || "") + ", " + (v.country || "") + "</b><br>" + new Date(v.timestamp).toLocaleDateString());
          markers.addLayer(m);
        }
      });

      markers.addTo(map);
    })
    .catch(function(err) {
      document.getElementById("visitor-count").textContent = "Map loading...";
    });
})();
</script>
