<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Berbagi Lokasi</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
    body {
      margin: 0;
    }
  </style>
</head>
<body>
  <div id="map"></div>

  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
  <script>
    // Buat peta
    const map = L.map('map').setView([0, 0], 2);

    // Tambahkan layer peta
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 19,
    }).addTo(map);

    // Ambil lokasi pengguna (dengan izin)
    if (navigator.geolocation) {
      navigator.geolocation.watchPosition(
        function(position) {
          const lat = position.coords.latitude;
          const lng = position.coords.longitude;
          
          map.setView([lat, lng], 15);
          L.marker([lat, lng]).addTo(map).bindPopup("Lokasi kamu").openPopup();
        },
        function(error) {
          alert("Gagal mendapatkan lokasi: " + error.message);
        }
      );
    } else {
      alert("Browser tidak mendukung geolokasi.");
    }
  </script>
</body>
</html>
