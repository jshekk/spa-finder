<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Spa Finder — No Website</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f4f6f9;
      color: #222;
    }

    header {
      background: #2c3e50;
      color: white;
      padding: 24px 32px;
    }

    header h1 { font-size: 1.6rem; font-weight: 600; }
    header p  { font-size: 0.9rem; opacity: 0.7; margin-top: 4px; }

    .controls {
      background: white;
      padding: 20px 32px;
      display: flex;
      gap: 12px;
      align-items: center;
      flex-wrap: wrap;
      border-bottom: 1px solid #ddd;
    }

    .controls input {
      flex: 1;
      min-width: 220px;
      padding: 10px 14px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 0.95rem;
    }

    .controls select {
      padding: 10px 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 0.95rem;
      background: white;
    }

    .controls button {
      padding: 10px 22px;
      background: #2c3e50;
      color: white;
      border: none;
      border-radius: 6px;
      font-size: 0.95rem;
      cursor: pointer;
      transition: background 0.2s;
    }

    .controls button:hover { background: #1a252f; }

    #status {
      padding: 12px 32px;
      font-size: 0.88rem;
      color: #555;
      min-height: 36px;
    }

    #results {
      padding: 0 32px 40px;
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 16px;
    }

    .card {
      background: white;
      border-radius: 10px;
      padding: 18px 20px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.08);
      border-left: 4px solid #e67e22;
    }

    .card h3 {
      font-size: 1rem;
      font-weight: 600;
      margin-bottom: 6px;
    }

    .card .address {
      font-size: 0.85rem;
      color: #666;
      margin-bottom: 6px;
    }

    .card .phone {
      font-size: 0.85rem;
      color: #2980b9;
      margin-bottom: 4px;
    }

    .card .rating {
      font-size: 0.8rem;
      color: #888;
      margin-top: 4px;
    }

    .card .badge {
      display: inline-block;
      margin-top: 10px;
      font-size: 0.75rem;
      background: #fef3e2;
      color: #c0392b;
      border-radius: 4px;
      padding: 2px 8px;
    }

    .empty {
      grid-column: 1 / -1;
      text-align: center;
      color: #999;
      padding: 60px 0;
      font-size: 1rem;
    }

    #map { width: 100%; height: 360px; }

    .export-bar {
      padding: 12px 32px;
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .export-bar button {
      padding: 8px 18px;
      border: 1px solid #2c3e50;
      background: white;
      color: #2c3e50;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.88rem;
    }

    .export-bar button:hover { background: #f0f0f0; }

    #count { font-size: 0.88rem; color: #555; }
  </style>
</head>
<body>

<header>
  <h1>Spa &amp; Med Spa Finder — No Website</h1>
  <p>Find spas and medical businesses within a radius that have no website listed on Google.</p>
</header>

<div class="controls">
  <input type="text" id="addressInput" placeholder="Enter zip code or city (e.g. Austin, TX)" />
  <select id="radius">
    <option value="25">25 miles</option>
    <option value="50" selected>50 miles</option>
    <option value="75">75 miles</option>
    <option value="100">100 miles</option>
  </select>
  <select id="bizType">
    <option value="spa">Spas</option>
    <option value="doctor">Medical / Clinics</option>
    <option value="health">Health &amp; Wellness</option>
    <option value="beauty_salon">Beauty Salons</option>
  </select>
  <button onclick="search()">Search</button>
</div>

<div id="map"></div>
<div id="status">Enter a location and click Search.</div>

<div class="export-bar">
  <span id="count"></span>
  <button onclick="exportCSV()">⬇ Export CSV</button>
</div>

<div id="results"></div>

<!-- Replace YOUR_API_KEY with your Google Maps API key -->
<script src="[maps.googleapis.com](https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places)"></script>

<script>
  let map, service, geocoder;
  let allResults = [];
  let pendingDetails = 0;
  let totalFetched = 0;

  function initMap(lat, lng) {
    map = new google.maps.Map(document.getElementById('map'), {
      center: { lat, lng },
      zoom: 10,
      styles: [{ featureType: 'poi', stylers: [{ visibility: 'off' }] }]
    });
  }

  function metersFromMiles(miles) {
    return miles * 1609.34;
  }

  function search() {
    const address = document.getElementById('addressInput').value.trim();
    const radiusMiles = parseInt(document.getElementById('radius').value);
    const bizType = document.getElementById('bizType').value;

    if (!address) {
      setStatus('Please enter a location.');
      return;
    }

    setStatus('Geocoding address...');
    allResults = [];
    totalFetched = 0;
    pendingDetails = 0;
    document.getElementById('results').innerHTML = '';
    document.getElementById('count').textContent = '';

    geocoder = geocoder || new google.maps.Geocoder();
    geocoder.geocode({ address }, (geoResults, status) => {
      if (status !== 'OK' || !geoResults.length) {
        setStatus('Could not find that location. Try a zip code or city name.');
        return;
      }

      const loc = geoResults[0].geometry.location;
      const center = { lat: loc.lat(), lng: loc.lng() };

      initMap(center.lat, center.lng);

      new google.maps.Circle({
        map,
        center,
        radius: metersFromMiles(radiusMiles),
        fillColor: '#2c3e50',
        fillOpacity: 0.05,
        strokeColor: '#2c3e50',
        strokeOpacity: 0.3,
        strokeWeight: 1
      });

      setStatus('Searching nearby businesses...');
      service = new google.maps.places.PlacesService(map);
      doNearbySearch(center, radiusMiles, bizType, null);
    });
  }

  function doNearbySearch(center, radiusMiles, bizType, pageToken) {
    const request = {
      location: center,
      radius: metersFromMiles(radiusMiles),
      type: bizType,
      ...(pageToken ? { pageToken } : {})
    };

    service.nearbySearch(request, (results, status, pagination) => {
      if (status === google.maps.places.PlacesServiceStatus.OK) {
        totalFetched += results.length;
        setStatus(`Found ${totalFetched} businesses so far — checking for websites...`);
        fetchDetails(results);

        if (pagination && pagination.hasNextPage && totalFetched < 60) {
          setTimeout(() => pagination.nextPage(), 1500);
        }
      } else if (status === google.maps.places.PlacesServiceStatus.ZERO_RESULTS) {
        setStatus('No results found for this area and category.');
      } else {
        setStatus(`Places API error: ${status}. Check your API key and billing.`);
      }
    });
  }

  // Fetch full place details to check for website field
  function fetchDetails(places) {
    places.forEach(place => {
      pendingDetails++;
      service.getDetails(
        {
          placeId: place.place_id,
          fields: ['name', 'vicinity', 'formatted_address', 'formatted_phone_number', 'website', 'rating', 'user_ratings_total', 'geometry']
        },
        (detail, status) => {
          pendingDetails--;

          if (status === google.maps.places.PlacesServiceStatus.OK) {
            // Only keep businesses with NO website
            if (!detail.website) {
              const entry = {
                name: detail.name,
                address: detail.formatted_address || detail.vicinity || 'N/A',
                phone: detail.formatted_phone_number || 'N/A',
                rating: detail.rating ? `⭐ ${detail.rating} (${detail.user_ratings_total || 0} reviews)` : 'No rating',
                lat: detail.geometry.location.lat(),
                lng: detail.geometry.location.lng()
              };

              allResults.push(entry);
              renderCard(entry);
              addMarker(entry);
              document.getElementById('count').textContent = `${allResults.length} businesses with no website`;
            }
          }

          if (pendingDetails === 0) {
            setStatus(`Done. ${allResults.length} of ${totalFetched} businesses have no website listed.`);
          }
        }
      );
    });
  }

  function addMarker(entry) {
    const marker = new google.maps.Marker({
      map,
      position: { lat: entry.lat, lng: entry.lng },
      title: entry.name,
      icon: {
        path: google.maps.SymbolPath.CIRCLE,
        scale: 7,
        fillColor: '#e67e22',
        fillOpacity: 0.9,
        strokeColor: 'white',
        strokeWeight: 1.5
      }
    });

    const infoWindow = new google.maps.InfoWindow({
      content: `<strong>${entry.name}</strong><br>${entry.address}<br>📞 ${entry.phone}<br><em style="color:#c0392b">No website</em>`
    });

    marker.addListener('click', () => infoWindow.open(map, marker));
  }

  function renderCard(b) {
    const container = document.getElementById('results');

    // Remove empty state if present
    const empty = container.querySelector('.empty');
    if (empty) empty.remove();

    const card = document.createElement('div');
    card.className = 'card';
    card.innerHTML = `
      <h3>${b.name}</h3>
      <div class="address">📍 ${b.address}</div>
      ${b.phone !== 'N/A' ? `<div class="phone">📞 ${b.phone}</div>` : ''}
      <div class="rating">${b.rating}</div>
      <span class="badge">🌐 No Website</span>
    `;
    container.appendChild(card);
  }

  function exportCSV() {
    if (!allResults.length) {
      alert('No results to export yet.');
      return;
    }
    const header = ['Name', 'Address', 'Phone', 'Rating'];
    const rows = allResults.map(b =>
      [b.name, b.address, b.phone, b.rating].map(v => `"${v.replace(/"/g, '""')}"`).join(',')
    );
    const csv = [header.join(','), ...rows].join('\n');
    const blob = new Blob([csv], { type: 'text/csv' });
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = 'no_website_spas.csv';
    a.click();
  }

  function setStatus(msg) {
    document.getElementById('status').textContent = msg;
  }
</script>

</body>
</html>
