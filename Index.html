# GeoGuardian
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GeoGuardian</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Leaflet CSS & JS for interactive maps -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin=""/>
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>

    <style>
        /* Custom styles for the application */
        body {
            font-family: 'Inter', sans-serif;
            overflow: hidden;
            background-color: #111827; /* bg-gray-900 */
        }
        #map {
            height: 100vh;
            width: 100vw;
            /* Fix for dark map tiles flashing white on load */
            background-color: #1f2937;
        }
        
        /* Dark Mode Popups */
        .leaflet-popup-content-wrapper {
            background: #1f2937; /* bg-gray-800 */
            color: #f3f4f6; /* text-gray-100 */
            border-radius: 8px;
            border: 1px solid #374151; /* bg-gray-700 */
        }
        .leaflet-popup-tip {
            background: #1f2937;
        }
        
        /* Dark Mode Legend */
        .legend {
            padding: 10px;
            line-height: 1.8;
            background: rgba(31, 41, 55, 0.9); /* bg-gray-800 90% opacity */
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(0,0,0,0.5);
            color: #f3f4f6; /* text-gray-100 */
            border: 1px solid #374151;
        }
        .legend strong {
            color: white;
        }
        .legend i {
            width: 18px;
            height: 18px;
            float: left;
            margin-right: 8px;
            opacity: 0.9;
            border-radius: 50%;
        }
    </style>
</head>
<body class="bg-gray-900">

    <!-- Login Modal (Initial Screen) -->
    <!-- MODIFICACIÓN: El modal de inicio de sesión ha sido eliminado -->
    
    <!-- Map Container -->
    <div id="map" class="relative"></div>

    <!-- Floating App Header -->
    <div class="absolute top-0 left-0 right-0 z-[1000] p-4 bg-gray-900/80 backdrop-blur-sm text-white shadow-lg text-center">
        <h1 class="text-xl font-bold">GeoGuardian (Demo Global)</h1>
    </div>

    <!-- Routing and Input Panel -->
    <!-- MODIFICACIÓN: Panel de trazar ruta eliminado -->

    <!-- Floating Action Button to Report Incident -->
    <div class="absolute bottom-6 right-6 z-[1000]">
        <button id="report-button" class="bg-red-600 text-white font-bold py-4 px-4 rounded-full shadow-lg hover:bg-red-700 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
            </svg>
        </button>
    </div>

    <!-- Alert Modal (for messages) -->
    <div id="alert-modal" class="hidden fixed inset-0 bg-black bg-opacity-70 z-[2000] flex justify-center items-center p-4 transition-opacity duration-300">
        <div class="bg-gray-800 border border-gray-700 rounded-lg shadow-2xl p-6 w-full max-w-sm text-center transform scale-95 transition-transform duration-300">
            <div id="alert-icon-container" class="mx-auto flex items-center justify-center h-16 w-16 rounded-full mb-4"></div>
            <h3 id="alert-title" class="text-xl font-semibold text-white"></h3>
            <p id="alert-message" class="text-gray-300 mt-2"></p>
            <button id="close-modal-button" class="mt-6 w-full bg-blue-600 text-white py-2 rounded-lg hover:bg-blue-700 transition-colors focus:outline-none focus:ring-2 focus:ring-blue-500">
                Entendido
            </button>
        </div>
    </div>


<script>
    // --- CONSTANTS AND CONFIGURATION ---
    const MIN_ZOOM_CIRCLES = 13; // Circles visible up to this zoom level (inclusive)
    const MAX_ZOOM_POLICE = 14; // Police markers visible from this zoom level (inclusive)

    // Center the map on a generic, major city location (e.g., Mexico City)
    const initialCoords = [19.4326, -99.1332]; // Mexico City
    
    // Safety Zone Colors
    const ZONE_COLORS = {
        'insegura': { color: '#ef4444', fillColor: '#ef4444', fillOpacity: 0.15 }, // Red
        'regular': { color: '#f97316', fillColor: '#f97316', fillOpacity: 0.10 }, // Orange
        'segura': { color: '#10b981', fillColor: '#10b981', fillOpacity: 0.05 }  // Green
    };

    // --- MOCK DATA ---
    const safetyZones = [
        // Simulated Insecure Zone (Red) - downtown
        { lat: 19.432, lon: -99.141, radius: 600, level: 'insegura', name: 'Zona Centro Histórico' },
        // Simulated Regular Zone (Orange) - commercial area
        { lat: 19.42, lon: -99.17, radius: 800, level: 'regular', name: 'Área de Negocios' },
        // Simulated Safe Zone (Green) - residential
        { lat: 19.40, lon: -99.11, radius: 1000, level: 'segura', name: 'Barrio Residencial' }
    ];

    const policeLocations = [
        { lat: 19.435, lon: -99.135 },
        { lat: 19.428, lon: -99.150 },
        { lat: 19.405, lon: -99.115 },
        { lat: 19.440, lon: -99.110 }
    ];

    // --- ICONS ---
    const policeIcon = L.icon({
        iconUrl: 'https://api.iconify.design/maki/police.svg?color=%2393c5fd', // Light Blue
        iconSize: [35, 35],
        className: 'police-marker'
    });

    const userIcon = L.icon({
        iconUrl: 'https://api.iconify.design/heroicons-solid/location-marker.svg?color=%2334d399', // Green Marker
        iconSize: [40, 40]
    });

    // --- GLOBAL MAP VARIABLES ---
    let map = null;
    let zoneLayers = [];
    let policeMarkers = [];
    // MODIFICACIÓN: 'routeLayers' eliminada
    let userMarker = null;

    // --- CORE FUNCTIONS ---

    // 1. Map Initialization
    function initializeMap() {
        map = L.map('map').setView(initialCoords, 12); // Start at a wide view (Zoom 12)

        // Dark map tile layer with bright features for contrast (CartoDB DarkMatter)
        L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
            maxZoom: 19,
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>'
        }).addTo(map);

        L.control.scale({ imperial: false }).addTo(map);

        // Place user marker
        userMarker = L.marker(initialCoords, { icon: userIcon }).addTo(map)
            .bindPopup('<b>Tu Ubicación</b>').openPopup();

        // Add event listener for zoom changes
        map.on('zoomend', handleZoomLevel);
        
        // Initial call to set visibility based on starting zoom
        displaySafetyZones(); 
        displayPoliceMarkers(false);
        handleZoomLevel();
        
        // MODIFICACIÓN: Mover la adición de la leyenda aquí
        // Esto asegura que se añade DESPUÉS de que 'map' esté inicializado
        legend.addTo(map);
    }

    // 2. Display Safety Zones (Circles)
    function displaySafetyZones() {
        // Clear existing circles
        zoneLayers.forEach(layer => map.removeLayer(layer));
        zoneLayers = [];

        safetyZones.forEach(zone => {
            const style = ZONE_COLORS[zone.level];
            
            const circle = L.circle([zone.lat, zone.lon], {
                color: style.color,
                fillColor: style.fillColor,
                fillOpacity: style.fillOpacity,
                weight: 1.5,
                radius: zone.radius, // Radius in meters
            }).addTo(map)
            .bindPopup(<b>Zona ${zone.level.toUpperCase()}</b><br>${zone.name}, { className: 'custom-popup' });
            
            zoneLayers.push(circle);
        });
    }
    
    // 3. Display Police Markers
    function displayPoliceMarkers(isVisible) {
        // Clear existing police markers if they exist
        policeMarkers.forEach(marker => map.removeLayer(marker));
        policeMarkers = [];

        if (isVisible) {
            policeLocations.forEach(loc => {
                const marker = L.marker([loc.lat, loc.lon], { icon: policeIcon }).addTo(map)
                    .bindPopup('<b>Policía</b><br>Patrullando la zona.');
                policeMarkers.push(marker);
            });
        }
    }

    // 4. Handle Zoom Level Visibility Logic
    function handleZoomLevel() {
        const currentZoom = map.getZoom();

        // Check if circles should be visible (Wide view)
        const circlesVisible = currentZoom <= MIN_ZOOM_CIRCLES;
        zoneLayers.forEach(layer => {
            if (circlesVisible) {
                if (!map.hasLayer(layer)) map.addLayer(layer);
            } else {
                if (map.hasLayer(layer)) map.removeLayer(layer);
            }
        });

        // Check if police should be visible (Close view)
        const policeVisible = currentZoom >= MAX_ZOOM_POLICE;
        displayPoliceMarkers(policeVisible);
    }
    
    // 5. Simulate Secure Route Tracing
    // MODIFICACIÓN: Función 'traceSecureRoute' eliminada

    // 6. UI/Modal Functions
    const modal = document.getElementById('alert-modal');
    const modalTitle = document.getElementById('alert-title');
    const modalMessage = document.getElementById('alert-message');
    const modalIconContainer = document.getElementById('alert-icon-container');

    const icons = {
        warning: <svg class="h-10 w-10 text-yellow-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" /></svg>,
        error: <svg class="h-10 w-10 text-red-500" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2 2m2-2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>,
        success: <svg class="h-10 w-10 text-green-500" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
    };
    
    const iconColors = {
        warning: 'bg-yellow-900 bg-opacity-50 border border-yellow-700',
        error: 'bg-red-900 bg-opacity-50 border border-red-700',
        success: 'bg-green-900 bg-opacity-50 border border-green-700'
    };

    function showAlert(title, message, type = 'warning') {
        modalTitle.textContent = title;
        modalMessage.textContent = message;
        modalIconContainer.innerHTML = icons[type];
        
        modalIconContainer.className = 'mx-auto flex items-center justify-center h-16 w-16 rounded-full mb-4';
        modalIconContainer.classList.add(...iconColors[type].split(' '));
        
        modal.classList.remove('hidden');
        setTimeout(() => {
            modal.querySelector('div').classList.remove('scale-95');
            modal.classList.remove('opacity-0');
        }, 10);
    }

    function hideModal() {
        modal.querySelector('div').classList.add('scale-95');
        modal.classList.add('opacity-0');
        setTimeout(() => modal.classList.add('hidden'), 300);
    }
    
    // 7. Legend Control
    const legend = L.control({position: 'bottomleft'});
    legend.onAdd = function (map) {
        const div = L.DomUtil.create('div', 'info legend');
        const items = {
            'Tu Ubicación': '#34d399',
            'Policía': '#93c5fd',
            // MODIFICACIÓN: Leyenda de ruta eliminada
            'Zona Insegura (Roja)': '#ef4444',
            'Zona Regular (Naranja)': '#f97316',
            'Zona Segura (Verde)': '#10b981'
        };
        let labels = ['<strong>Leyenda</strong>'];
        for (let key in items) { labels.push('<i style="background:' + items[key] + '"></i> ' + key); }
        div.innerHTML = labels.join('<br>');
        return div;
    };
    // MODIFICACIÓN: La línea 'legend.addTo(map);' se movió de aquí
    // a dentro de la función initializeMap() para evitar el error.

    // --- EVENT LISTENERS ---
    // MODIFICACIÓN: Eliminado el listener del 'login-button'
    
    document.getElementById('close-modal-button').addEventListener('click', hideModal);
    // MODIFICACIÓN: Event listener de 'trace-route-button' eliminado
    
    document.getElementById('report-button').addEventListener('click', () => {
        showAlert('Reporte de Emergencia', 'Esta función simula el envío de una alerta o llamada de emergencia a los servicios locales.', 'error');
    });

    // MODIFICACIÓN: Inicializar el mapa al cargar la ventana, ya que se eliminó el inicio de sesión
    window.onload = () => {
        initializeMap();
        showAlert('Bienvenido a GeoGuardian', 'Este es un mapa de demostración global. Usa el zoom para alternar entre las zonas de seguridad (vista amplia) y las patrullas policiales (vista de acercamiento).', 'success');
    };

</script>
</body>
</html>
