<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Safir's Music</title>
    <style>
        :root {
            --primary-color: #1db954;
            --bg-color: #121212;
            --card-bg: #181818;
            --text-color: #b3b3b3;
            --text-white: #ffffff;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-white);
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* Header & Navigation */
        header {
            background-color: #000000;
            padding: 20px;
            text-align: center;
        }

        h1 {
            margin: 0;
            color: var(--primary-color);
            font-size: 2.5rem;
            cursor: pointer;
        }

        nav {
            margin-top: 20px;
            display: flex;
            justify-content: center;
            gap: 20px;
        }

        .nav-btn {
            background: none;
            border: none;
            color: var(--text-color);
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            padding: 10px 20px;
            border-radius: 20px;
            transition: all 0.3s ease;
        }

        .nav-btn:hover, .nav-btn.active {
            color: var(--text-white);
            background-color: #282828;
        }

        /* Main Content */
        main {
            flex: 1;
            padding: 40px;
            max-width: 800px;
            margin: 0 auto;
            width: 100%;
            box-sizing: border-box;
            padding-bottom: 100px; /* Space for player */
        }

        .section {
            display: none;
            animation: fadeIn 0.5s;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Add Song Section */
        .upload-area {
            border: 2px dashed var(--text-color);
            border-radius: 10px;
            padding: 50px;
            text-align: center;
            transition: border-color 0.3s;
        }

        .upload-area:hover {
            border-color: var(--primary-color);
        }

        .file-input {
            display: none;
        }

        .add-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.2rem;
            border-radius: 30px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s;
        }

        .add-btn:hover {
            background-color: #1ed760;
            transform: scale(1.05);
        }

        /* Library Controls */
        .library-controls {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 30px;
        }

        .search-input {
            width: 100%;
            padding: 12px;
            border-radius: 20px;
            border: none;
            background-color: #282828;
            color: white;
            font-size: 1rem;
            box-sizing: border-box;
            outline: none;
        }

        .search-input:focus {
            box-shadow: 0 0 0 2px var(--primary-color);
        }

        /* Playlist List */
        .playlist-list {
            list-style: none;
            padding: 0;
            margin-bottom: 30px;
        }

        .playlist-item {
            background-color: var(--card-bg);
            padding: 15px;
            margin-bottom: 8px;
            border-radius: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .playlist-item:hover {
            background-color: #282828;
        }

        .playlist-name {
            font-weight: bold;
            font-size: 1.1rem;
            flex: 1;
        }

        /* Boutons d'action playlist */
        .playlist-actions {
            display: flex;
            gap: 5px;
        }

        .edit-btn, .delete-pl-btn {
            background: none;
            border: none;
            color: var(--text-color);
            font-size: 1.2rem;
            cursor: pointer;
            padding: 5px 10px;
            border-radius: 50%;
        }

        .edit-btn:hover { color: var(--primary-color); }
        .delete-pl-btn:hover { color: #ff4d4d; background-color: rgba(255, 255, 255, 0.1); }


        /* Library Section */
        .library-list {
            list-style: none;
            padding: 0;
        }

        .song-item {
            background-color: var(--card-bg);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            transition: background-color 0.3s;
        }

        .song-item:hover {
            background-color: #282828;
        }

        .song-info {
            display: flex;
            align-items: center;
            gap: 15px;
            flex: 1;
            cursor: pointer;
            min-width: 0;
        }

        .song-icon {
            font-size: 1.5rem;
        }

        .song-title {
            font-size: 1rem;
            font-weight: 500;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .song-actions {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .delete-btn {
            background-color: transparent;
            color: var(--text-color);
            border: none;
            cursor: pointer;
            font-size: 1.2rem;
            padding: 5px 10px;
            border-radius: 50%;
        }

        .delete-btn:hover {
            color: #ff4d4d;
            background-color: rgba(255, 255, 255, 0.1);
        }

        /* Move Button */
        .move-btn {
            background: none;
            border: none;
            padding: 5px;
            cursor: pointer;
            display: flex;
            align-items: center;
            opacity: 0.7;
            transition: opacity 0.2s;
        }

        .move-btn:hover { opacity: 1; }

        .move-btn img {
            width: 20px;
            height: 20px;
            filter: invert(1);
        }

        /* Dropdown Menu */
        .dropdown-menu {
            position: absolute;
            background-color: #282828;
            border-radius: 5px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
            z-index: 1000;
            display: none;
            min-width: 150px;
            overflow: hidden;
        }

        .dropdown-item {
            padding: 10px 15px;
            cursor: pointer;
            font-size: 0.9rem;
            color: var(--text-white);
        }

        .dropdown-item:hover {
            background-color: var(--primary-color);
        }

        /* Modal for Creating Playlist */
        .modal {
            display: none; 
            position: fixed; 
            z-index: 2000; 
            left: 0;
            top: 0;
            width: 100%; 
            height: 100%; 
            overflow: auto; 
            background-color: rgba(0,0,0,0.8); 
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background-color: #282828;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
            position: relative;
        }

        .modal-close {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-color);
        }

        .modal-title {
            margin-top: 0;
            color: var(--primary-color);
        }

        .modal-input {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            border: none;
            background-color: #3e3e3e;
            color: white;
            font-size: 1rem;
            box-sizing: border-box;
        }

        .song-select-list {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 20px;
        }

        .song-select-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px;
            cursor: pointer;
            border-radius: 4px;
        }

        .song-select-item:hover {
            background-color: #3e3e3e;
        }

        /* Player Bar */
        .player-bar {
            background-color: #181818;
            padding: 15px;
            text-align: center;
            border-top: 1px solid #282828;
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            display: none;
        }

        .player-bar.active {
            display: block;
        }

        audio {
            width: 100%;
            max-width: 600px;
        }
        
        .section-title {
            color: var(--text-color);
            margin-bottom: 15px;
            font-size: 1.2rem;
            cursor: pointer;
            display: inline-block;
        }
        
        .section-title:hover {
            text-decoration: underline;
        }

    </style>
</head>
<body>

    <header>
        <h1 onclick="resetView(); showSection('library');">Safir's Music</h1>
        <nav>
            <button class="nav-btn active" onclick="showSection('add')">Add Songs</button>
            <button class="nav-btn" onclick="showSection('library')">Library</button>
        </nav>
    </header>

    <main>
        <!-- Section Add Songs -->
        <div id="add-section" class="section active">
            <div class="upload-area">
                <h2>Importer une musique</h2>
                <p>Formats supportés : MP3, WAV, OGG</p>
                <br>
                <input type="file" id="fileInput" class="file-input" accept="audio/*" multiple>
                <button class="add-btn" onclick="document.getElementById('fileInput').click()">Add Song</button>
            </div>
            <p id="status-msg" style="text-align: center; margin-top: 20px; color: var(--primary-color);"></p>
        </div>

        <!-- Section Library -->
        <div id="library-section" class="section">
            
            <div class="library-controls">
                <input type="text" id="search-input" class="search-input" placeholder="Rechercher une chanson..." oninput="handleSearch()">
                <button class="add-btn" style="width: 100%; padding: 12px;" onclick="openCreateModal()">Create Playlist</button>
            </div>

            <!-- Playlist List -->
            <div id="playlists-container">
                <h3 class="section-title">Playlists</h3>
                <ul class="playlist-list" id="playlist-list">
                    <!-- Playlists ici -->
                </ul>
            </div>

            <!-- Song List -->
            <div id="songs-container">
                <h3 class="section-title" id="current-view-title">Toutes les chansons</h3>
                <ul class="library-list" id="song-list">
                    <!-- Chansons ici -->
                </ul>
                <p id="empty-msg" style="display:none; color: var(--text-color); text-align:center; margin-top: 20px;">Aucune chanson.</p>
            </div>
            
        </div>
    </main>

    <!-- Modal pour créer une playlist -->
    <div id="create-modal" class="modal">
        <div class="modal-content">
            <span class="modal-close" onclick="closeCreateModal()">&times;</span>
            <h2 class="modal-title">Nouvelle Playlist</h2>
            <input type="text" id="playlist-name-input" class="modal-input" placeholder="Nom de la playlist">
            
            <p style="color:var(--text-color); margin-bottom: 10px;">Sélectionner des chansons (déplacées vers la playlist) :</p>
            <div class="song-select-list" id="modal-song-list">
                <!-- Liste pour sélection -->
            </div>
            <button class="add-btn" style="width: 100%;" onclick="saveNewPlaylist()">Créer</button>
        </div>
    </div>

    <!-- Barre de lecture -->
    <div class="player-bar" id="player-bar">
        <div id="now-playing" style="margin-bottom: 10px; color: white;">En cours de lecture...</div>
        <audio id="audio-player" controls></audio>
    </div>

    <!-- Menu Dropdown pour déplacer les chansons -->
    <div id="dropdown-menu" class="dropdown-menu"></div>

    <script>
        // --- GESTION DE INDEXEDDB ---
        let db;
        const dbName = "SafirMusicDB";
        const songStoreName = "songs";
        const playlistStoreName = "playlists";

        // Variables d'état
        let currentViewPlaylistId = null; 
        let allSongsCache = [];
        let allPlaylistsCache = [];
        let currentPlayingId = null; // Pour suivre quelle chanson joue

        // 1. Ouvrir ou Créer la Base de Données
        const request = indexedDB.open(dbName, 2);

        request.onerror = (event) => {
            console.error("Erreur ouverture DB:", event.target.error);
        };

        request.onsuccess = (event) => {
            db = event.target.result;
            console.log("DB ouverte avec succès");
            initLibrary();
            
            // --- ECOUTEUR AUTOPLAY ---
            const audioPlayer = document.getElementById('audio-player');
            audioPlayer.addEventListener('ended', playNextSong);
        };

        request.onupgradeneeded = (event) => {
            db = event.target.result;
            
            if (!db.objectStoreNames.contains(songStoreName)) {
                const songStore = db.createObjectStore(songStoreName, { keyPath: 'id', autoIncrement: true });
                songStore.createIndex('playlistId', 'playlistId', { unique: false });
            }
            
            if (!db.objectStoreNames.contains(playlistStoreName)) {
                const playlistStore = db.createObjectStore(playlistStoreName, { keyPath: 'id', autoIncrement: true });
            }
        };

        // --- FONCTIONS LOGIQUES ---

        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => section.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));

            const section = document.getElementById(sectionId + '-section');
            if(section) section.classList.add('active');

            const buttons = document.querySelectorAll('.nav-btn');
            if (sectionId === 'add') buttons[0].classList.add('active');
            if (sectionId === 'library') {
                buttons[1].classList.add('active');
                resetView();
            }
        }

        function resetView() {
            currentViewPlaylistId = null;
            document.getElementById('current-view-title').textContent = "Toutes les chansons";
            document.getElementById('search-input').value = "";
            renderSongs();
        }

        function initLibrary() {
            const transaction = db.transaction([songStoreName, playlistStoreName], 'readonly');
            const songStore = transaction.objectStore(songStoreName);
            const playlistStore = transaction.objectStore(playlistStoreName);

            const songReq = songStore.getAll();
            const playlistReq = playlistStore.getAll();

            songReq.onsuccess = (e) => { allSongsCache = e.target.result; checkReady(); };
            playlistReq.onsuccess = (e) => { allPlaylistsCache = e.target.result; checkReady(); };

            function checkReady() {
                if (songReq.readyState === 'done' && playlistReq.readyState === 'done') {
                    renderPlaylists();
                    renderSongs();
                }
            }
        }

        // --- AFFICHAGE ---

        function renderPlaylists() {
            const listContainer = document.getElementById('playlist-list');
            listContainer.innerHTML = '';

            if (allPlaylistsCache.length === 0) {
                listContainer.innerHTML = '<li style="color:var(--text-color); font-size:0.9rem; cursor:default;">Aucune playlist créée.</li>';
                return;
            }

            allPlaylistsCache.forEach(playlist => {
                const li = document.createElement('li');
                li.className = 'playlist-item';
                li.onclick = (e) => {
                    // Si on clique sur un bouton d'action, on n'ouvre pas la playlist
                    if(e.target.closest('button')) return; 
                    openPlaylistView(playlist.id, playlist.name);
                };

                li.innerHTML = `
                    <span class="playlist-name">📁 ${playlist.name}</span>
                    <div class="playlist-actions">
                        <button class="edit-btn" onclick="editPlaylistName(${playlist.id}, '${playlist.name.replace(/'/g, "\\'")}')">✏️</button>
                        <button class="delete-pl-btn" onclick="deletePlaylist(${playlist.id})">✕</button>
                    </div>
                `;
                listContainer.appendChild(li);
            });
        }

        function openPlaylistView(playlistId, playlistName) {
            currentViewPlaylistId = playlistId;
            document.getElementById('current-view-title').textContent = `Playlist : ${playlistName}`;
            renderSongs();
        }

        function renderSongs() {
            const listContainer = document.getElementById('song-list');
            const emptyMsg = document.getElementById('empty-msg');
            const searchTerm = document.getElementById('search-input').value.toLowerCase();

            let songs = [...allSongsCache]; // Copie
            
            // Filtrer par vue
            if (currentViewPlaylistId === null) {
                // Vue Bibliothèque : chansons SANS playlistId
                songs = songs.filter(s => !s.playlistId);
            } else {
                // Vue Playlist : chansons AVEC ce playlistId
                songs = songs.filter(s => s.playlistId === currentViewPlaylistId);
            }

            // Filtrer par recherche
            if (searchTerm) {
                songs = songs.filter(s => s.name.toLowerCase().includes(searchTerm));
            }

            listContainer.innerHTML = '';

            if (songs.length === 0) {
                emptyMsg.style.display = 'block';
                listContainer.style.display = 'none';
                emptyMsg.textContent = currentViewPlaylistId ? "Cette playlist est vide." : "Aucune chanson pour le moment.";
            } else {
                emptyMsg.style.display = 'none';
                listContainer.style.display = 'block';

                songs.forEach(song => {
                    const li = document.createElement('li');
                    li.className = 'song-item';
                    
                    // Bouton Move visible seulement si on est dans la vue Bibliothèque (hors playlist)
                    const showMoveBtn = currentViewPlaylistId === null;

                    li.innerHTML = `
                        <div class="song-info" onclick="playSong(${song.id})">
                            <span class="song-icon">🎵</span>
                            <span class="song-title">${song.name}</span>
                        </div>
                        <div class="song-actions">
                            ${showMoveBtn ? `
                                <button class="move-btn" onclick="showMoveMenu(event, ${song.id})" title="Déplacer vers une playlist">
                                    <img src="https://z-cdn-media.chatglm.cn/files/ddf77dde-c127-4f28-aa75-dac1b2638d17.png?auth_key=1874534349-c0e74819139e4c5ca22a85cf5e510bd6-0-6c3348db41e070fbe14f455b9d5287a3" alt="Move">
                                </button>
                            ` : ''}
                            <button class="delete-btn" onclick="deleteSong(${song.id})">✕</button>
                        </div>
                    `;
                    listContainer.appendChild(li);
                });
            }
        }

        // --- ACTIONS DB ---

        const fileInput = document.getElementById('fileInput');
        fileInput.addEventListener('change', function(event) {
            const files = event.target.files;
            if (files.length > 0) {
                Array.from(files).forEach(file => addSongToDB(file));
            }
        });

        function addSongToDB(file) {
            const transaction = db.transaction([songStoreName], 'readwrite');
            const store = transaction.objectStore(songStoreName);
            const newSong = { name: file.name, data: file, playlistId: null };
            
            store.add(newSong);
            transaction.oncomplete = () => {
                const statusMsg = document.getElementById('status-msg');
                statusMsg.textContent = `Chanson "${file.name}" ajoutée !`;
                setTimeout(() => statusMsg.textContent = "", 3000);
                fileInput.value = '';
                initLibrary();
            };
        }

        function deleteSong(id) {
            const transaction = db.transaction([songStoreName], 'readwrite');
            const store = transaction.objectStore(songStoreName);
            store.delete(id);
            transaction.oncomplete = () => initLibrary();
        }

        // --- LOGIQUE PLAYLISTS ---

        function openCreateModal() {
            const modal = document.getElementById('create-modal');
            const songSelectList = document.getElementById('modal-song-list');
            document.getElementById('playlist-name-input').value = '';
            
            const availableSongs = allSongsCache.filter(s => !s.playlistId);
            
            songSelectList.innerHTML = '';
            if (availableSongs.length === 0) {
                songSelectList.innerHTML = '<p style="color:var(--text-color); text-align:center;">Aucune chanson disponible.</p>';
            } else {
                availableSongs.forEach(song => {
                    const div = document.createElement('div');
                    div.className = 'song-select-item';
                    div.innerHTML = `
                        <input type="checkbox" id="modal-song-${song.id}" value="${song.id}">
                        <label for="modal-song-${song.id}">🎵 ${song.name}</label>
                    `;
                    songSelectList.appendChild(div);
                });
            }
            
            modal.style.display = 'flex';
        }

        function closeCreateModal() {
            document.getElementById('create-modal').style.display = 'none';
        }

        function saveNewPlaylist() {
            const name = document.getElementById('playlist-name-input').value.trim();
            if (!name) { alert("Veuillez entrer un nom."); return; }

            const checkboxes = document.querySelectorAll('#modal-song-list input[type="checkbox"]:checked');
            const songIds = Array.from(checkboxes).map(cb => parseInt(cb.value));

            const transaction = db.transaction([playlistStoreName, songStoreName], 'readwrite');
            const playlistStore = transaction.objectStore(playlistStoreName);
            const playlistReq = playlistStore.add({ name: name });

            playlistReq.onsuccess = (e) => {
                const newPlaylistId = e.target.result;
                const songStore = transaction.objectStore(songStoreName);
                
                songIds.forEach(id => {
                    const getReq = songStore.get(id);
                    getReq.onsuccess = (e) => {
                        const song = e.target.result;
                        if (song) {
                            song.playlistId = newPlaylistId;
                            songStore.put(song);
                        }
                    };
                });
            };

            transaction.oncomplete = () => {
                closeCreateModal();
                initLibrary();
            };
        }

        // Supprimer Playlist ET ses chansons
        function deletePlaylist(playlistId) {
            if(!confirm("Supprimer cette playlist et toutes ses chansons ?")) return;

            const transaction = db.transaction([playlistStoreName, songStoreName], 'readwrite');
            const playlistStore = transaction.objectStore(playlistStoreName);
            const songStore = transaction.objectStore(songStoreName);

            // 1. Supprimer l'entrée playlist
            playlistStore.delete(playlistId);

            // 2. Trouver et supprimer les chansons associées
            // On utilise un curseur pour parcourir les chansons
            const request = songStore.openCursor();
            request.onsuccess = (event) => {
                const cursor = event.target.result;
                if (cursor) {
                    if (cursor.value.playlistId === playlistId) {
                        cursor.delete(); // Supprimer la chanson
                    }
                    cursor.continue();
                }
            };

            transaction.oncomplete = () => {
                // Si on était dans cette playlist, revenir à l'accueil
                if (currentViewPlaylistId === playlistId) {
                    resetView();
                }
                initLibrary();
            };
        }

        function editPlaylistName(id, currentName) {
            const newName = prompt("Nouveau nom:", currentName);
            if (newName && newName.trim() !== "") {
                const transaction = db.transaction([playlistStoreName], 'readwrite');
                const store = transaction.objectStore(playlistStoreName);
                const req = store.get(id);
                req.onsuccess = (e) => {
                    const playlist = e.target.result;
                    playlist.name = newName;
                    store.put(playlist);
                };
                transaction.oncomplete = () => initLibrary();
            }
        }

        // --- MOVE MENU ---
        
        function showMoveMenu(event, songId) {
            event.stopPropagation();
            const menu = document.getElementById('dropdown-menu');
            menu.innerHTML = '';

            if (allPlaylistsCache.length === 0) {
                alert("Pas de playlists");
                return;
            }

            allPlaylistsCache.forEach(p => {
                const item = document.createElement('div');
                item.className = 'dropdown-item';
                item.textContent = p.name;
                item.onclick = () => moveSongToPlaylist(songId, p.id);
                menu.appendChild(item);
            });

            const rect = event.target.getBoundingClientRect();
            menu.style.left = `${rect.left}px`;
            menu.style.top = `${rect.bottom + 5}px`;
            menu.style.display = 'block';
            
            setTimeout(() => {
                window.onclick = closeMenuOnClickOutside;
            }, 0);
        }

        function closeMenuOnClickOutside(e) {
            const menu = document.getElementById('dropdown-menu');
            if (!menu.contains(e.target)) {
                menu.style.display = 'none';
                window.onclick = null;
            }
        }

        function moveSongToPlaylist(songId, playlistId) {
            const transaction = db.transaction([songStoreName], 'readwrite');
            const store = transaction.objectStore(songStoreName);
            const req = store.get(songId);
            
            req.onsuccess = (e) => {
                const song = e.target.result;
                song.playlistId = playlistId;
                store.put(song);
            };
            
            transaction.oncomplete = () => {
                document.getElementById('dropdown-menu').style.display = 'none';
                initLibrary();
            };
        }

        function handleSearch() {
            renderSongs();
        }

        // --- LECTURE AUDIO & AUTOPLAY ---

        function playSong(id) {
            const song = allSongsCache.find(s => s.id === id);
            if (song) {
                currentPlayingId = id; // Mémoriser l'ID joué
                
                const audioPlayer = document.getElementById('audio-player');
                const playerBar = document.getElementById('player-bar');
                const nowPlaying = document.getElementById('now-playing');

                const blobUrl = URL.createObjectURL(song.data);
                audioPlayer.src = blobUrl;
                audioPlayer.play();
                
                nowPlaying.textContent = `Lecture : ${song.name}`;
                playerBar.classList.add('active');
            }
        }

        function playNextSong() {
            // Trouver la chanson qui vient de finir
            const currentSong = allSongsCache.find(s => s.id === currentPlayingId);
            if (!currentSong) return;

            // Déterminer la liste de lecture actuelle (Playlist ou Bibliothèque)
            let currentList;
            if (currentSong.playlistId) {
                // Si la chanson est dans une playlist, on filtre sur cette playlist
                currentList = allSongsCache.filter(s => s.playlistId === currentSong.playlistId);
            } else {
                // Sinon, on filtre sur la bibliothèque (chansons sans playlist)
                currentList = allSongsCache.filter(s => !s.playlistId);
            }

            // Trouver l'index de la chanson actuelle dans cette liste
            const currentIndex = currentList.findIndex(s => s.id === currentPlayingId);

            // S'il y a une chanson suivante dans la liste
            if (currentIndex !== -1 && currentIndex < currentList.length - 1) {
                const nextSong = currentList[currentIndex + 1];
                playSong(nextSong.id);
            }
        }
    </script>
</body>
</html>
