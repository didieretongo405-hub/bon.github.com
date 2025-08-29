<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestion des Rapports de Stage</title>
    <!-- Ajout de Font Awesome pour les icônes -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            color: #333;
        }

        .container {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* Header */
        header {
            background-color: #2c3e50;
            color: white;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .header-buttons {
            display: flex;
            gap: 1rem;
        }

        .header-buttons button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 4px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .header-buttons button:hover {
            background-color: #2980b9;
        }

        /* Main Content */
        .main-content {
            display: flex;
            flex: 1;
        }

        /* Sidebar */
        .sidebar {
            width: 250px;
            background-color: #34495e;
            color: white;
            padding: 1rem 0;
        }

        .sidebar ul {
            list-style: none;
        }

        .sidebar li {
            padding: 1rem 2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            transition: background-color 0.3s;
        }

        .sidebar li:hover {
            background-color: #2c3e50;
        }

        .sidebar li.active {
            background-color: #3498db;
        }

        /* Content Area */
        .content {
            flex: 1;
            padding: 2rem;
            overflow-y: auto;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Form Styles */
        .form-row {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .form-group {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .form-group label {
            margin-bottom: 0.5rem;
            font-weight: 500;
        }

        .form-group input,
        .form-group select {
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        .file-upload {
            margin-top: 0.5rem;
        }

        .file-label {
            display: inline-block;
            padding: 0.75rem 1.5rem;
            background-color: #3498db;
            color: white;
            border-radius: 4px;
            cursor: pointer;
            text-align: center;
        }

        .file-label:hover {
            background-color: #2980b9;
        }

        input[type="file"] {
            display: none;
        }

        .form-buttons {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .btn-primary {
            background-color: #2ecc71;
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }

        .btn-primary:hover {
            background-color: #27ae60;
        }

        .btn-secondary {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }

        .btn-secondary:hover {
            background-color: #c0392b;
        }

        /* Search Bar */
        .search-bar {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .search-bar input {
            flex: 1;
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        .search-bar button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 4px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .search-bar button:hover {
            background-color: #2980b9;
        }

        /* Filters */
        .filters {
            background-color: #f9f9f9;
            padding: 1.5rem;
            border-radius: 4px;
            margin-bottom: 1.5rem;
            border: 1px solid #eee;
        }

        .filters h3 {
            margin-bottom: 1rem;
        }

        .filter-group {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .filter-group label {
            min-width: 100px;
            font-weight: 500;
        }

        .filter-group input,
        .filter-group select {
            padding: 0.5rem;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        /* Tables */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1rem;
            background-color: white;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
        }

        th, td {
            padding: 0.75rem 1rem;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        th {
            background-color: #f5f5f5;
            font-weight: 600;
        }

        tr:hover {
            background-color: #f9f9f9;
        }

        /* Action buttons */
        .action-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1rem;
            margin-right: 0.5rem;
        }

        .view-btn {
            color: #3498db;
        }

        .edit-btn {
            color: #2ecc71;
        }

        .delete-btn {
            color: #e74c3c;
        }

        /* Departments */
        .departments-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .department-card {
            background-color: white;
            padding: 1.5rem;
            border-radius: 4px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            text-align: center;
        }

        .department-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .department-card h3 {
            color: #2c3e50;
            margin-bottom: 0.5rem;
        }

        .department-card p {
            color: #7f8c8d;
        }

        .department-results {
            margin-top: 2rem;
        }

        #dept-title {
            margin-bottom: 1rem;
        }

        #dept-title span {
            color: #3498db;
        }

        /* Sort options */
        .sort-options {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .sort-options select {
            padding: 0.5rem;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
        }

        .modal-content {
            background-color: white;
            margin: 10% auto;
            padding: 2rem;
            border-radius: 4px;
            width: 50%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            position: relative;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            position: absolute;
            right: 1rem;
            top: 0.5rem;
            cursor: pointer;
        }

        .close:hover {
            color: #000;
        }

        .modal textarea {
            width: 100%;
            height: 150px;
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin: 1rem 0;
            resize: vertical;
        }

        .modal-buttons {
            display: flex;
            gap: 1rem;
            justify-content: flex-end;
        }

        /* Notifications */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            border-radius: 4px;
            color: white;
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 1100;
        }

        .notification.success {
            background-color: #2ecc71;
        }

        .notification.error {
            background-color: #e74c3c;
        }

        .notification.show {
            opacity: 1;
        }

        /* Responsive adjustments */
        @media (max-width: 768px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
            }
            
            .form-row {
                flex-direction: column;
            }
            
            .modal-content {
                width: 90%;
            }

            .header-buttons {
                flex-direction: column;
                gap: 0.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header>
            <h1>Gestion des Rapports de Stage</h1>
            <div class="header-buttons">
                <button id="settings-btn"><i class="fas fa-cog"></i> Paramètres</button>
                <button id="profile-btn"><i class="fas fa-user"></i> Profil</button>
                <button id="logout-btn"><i class="fas fa-sign-out-alt"></i> Déconnexion</button>
            </div>
        </header>

        <div class="main-content">
            <!-- Sidebar -->
            <aside class="sidebar">
                <nav>
                    <ul>
                        <li class="active" data-tab="nouveau-rapport"><i class="fas fa-plus-circle"></i> Nouveau Rapport</li>
                        <li data-tab="recherche"><i class="fas fa-search"></i> Recherche</li>
                        <li data-tab="departements"><i class="fas fa-building"></i> Départements</li>
                        <li data-tab="rapports"><i class="fas fa-file-alt"></i> Tous les rapports</li>
                        <li data-tab="utilisateurs"><i class="fas fa-users"></i> Utilisateurs</li>
                    </ul>
                </nav>
            </aside>

            <!-- Content Area -->
            <main class="content">
                <!-- Nouveau Rapport Tab -->
                <div id="nouveau-rapport" class="tab-content active">
                    <h2>Nouveau Rapport de Stage</h2>
                    <form id="rapport-form">
                        <div class="form-row">
                            <div class="form-group">
                                <label for="nom">Nom stagiaire</label>
                                <input type="text" id="nom" required>
                            </div>
                            <div class="form-group">
                                <label for="prenom">Prénom stagiaire</label>
                                <input type="text" id="prenom" required>
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label for="email">Email</label>
                                <input type="email" id="email" required>
                            </div>
                            <div class="form-group">
                                <label for="telephone">Téléphone</label>
                                <input type="tel" id="telephone" required>
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label for="date-naissance">Date de naissance</label>
                                <input type="date" id="date-naissance" required>
                            </div>
                            <div class="form-group">
                                <label for="date-debut">Date début</label>
                                <input type="date" id="date-debut" required>
                            </div>
                            <div class="form-group">
                                <label for="date-fin">Date fin</label>
                                <input type="date" id="date-fin" required>
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label for="etablissement">Établissement</label>
                                <input type="text" id="etablissement" required>
                            </div>
                            <div class="form-group">
                                <label for="departement">Département</label>
                                <select id="departement" required>
                                    <option value="">Sélectionner un département</option>
                                    <option value="Informatique">Informatique</option>
                                    <option value="Ressources Humaines">Ressources Humaines</option>
                                    <option value="Comptabilité">Comptabilité</option>
                                    <option value="Maintenance">Maintenance</option>
                                    <option value="Direction">Direction</option>
                                    <option value="Achat">Achat</option>
                                    <option value="Communication">Communication</option>
                                    <option value="Centre de traitement des dechets">Centre de traitement des dechets</option>
                                    <option value="Magasin">Magasin</option>
                                    <option value="QHSE">QHSE</option>
                                    <option value="PU">PU</option>
                                    <option value="service juridique">Service juridique</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="fichier">Rapport (PDF)</label>
                            <div class="file-upload">
                                <input type="file" id="fichier" accept=".pdf" required>
                                <label for="fichier" class="file-label">Choisir un fichier</label>
                                <span id="file-name"></span>
                            </div>
                        </div>

                        <div class="form-buttons">
                            <button type="submit" class="btn-primary">Enregistrer</button>
                            <button type="reset" class="btn-secondary">Annuler</button>
                        </div>
                    </form>
                </div>

                <!-- Recherche Tab -->
                <div id="recherche" class="tab-content">
                    <h2>Recherche de Rapports</h2>
                    <div class="search-bar">
                        <input type="text" id="search-input" placeholder="Nom stagiaire, établissement, département...">
                        <button id="search-btn"><i class="fas fa-search"></i> Rechercher</button>
                    </div>

                    <div class="filters">
                        <h3>Filtres</h3>
                        <div class="filter-group">
                            <label for="filter-departement">Département:</label>
                            <select id="filter-departement">
                                <option value="">Tous</option>
                                <option value="Informatique">Informatique</option>
                                <option value="Ressources Humaines">Ressources Humaines</option>
                                <option value="Comptabilité">Comptabilité</option>
                                <option value="Maintenance">Maintenance</option>
                                <option value="Direction">Direction</option>
                                <option value="Achat">Achat</option>
                                <option value="Communication">Communication</option>
                                <option value="Centre de traitement des dechets">Centre de traitement des dechets</option>
                                <option value="Magasin">Magasin</option>
                                <option value="QHSE">QHSE</option>
                                <option value="PU">PU</option>
                                <option value="service juridique">Service juridique</option>
                            </select>
                        </div>

                        <div class="filter-group">
                            <label for="filter-etablissement">Établissement:</label>
                            <input type="text" id="filter-etablissement" placeholder="Nom de l'établissement">
                        </div>

                        <div class="filter-group">
                            <label for="filter-date-debut">Période:</label>
                            <input type="date" id="filter-date-debut" placeholder="Date début">
                            <span>à</span>
                            <input type="date" id="filter-date-fin" placeholder="Date fin">
                        </div>
                    </div>

                    <div class="results">
                        <h3>Résultats</h3>
                        <table id="results-table">
                            <thead>
                                <tr>
                                    <th>Nom</th>
                                    <th>Prénom</th>
                                    <th>Département</th>
                                    <th>Établissement</th>
                                    <th>Dates</th>
                                    <th>PDF</th>
                                    <th>Appréciation</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Les résultats seront ajoutés dynamiquement -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Départements Tab -->
                <div id="departements" class="tab-content">
                    <h2>Départements</h2>
                    <div class="departments-list">
                        <div class="department-card" data-dept="Informatique">
                            <h3>Informatique</h3>
                            <p>5 rapports</p>
                        </div>
                        <div class="department-card" data-dept="Ressources Humaines">
                            <h3>Ressources Humaines</h3>
                            <p>3 rapports</p>
                        </div>
                        <div class="department-card" data-dept="Comptabilité">
                            <h3>Comptabilité</h3>
                            <p>2 rapports</p>
                        </div>
                        <div class="department-card" data-dept="Maintenance">
                            <h3>Maintenance</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="Direction">
                            <h3>Direction</h3>
                            <p>1 rapport</p>
                        </div>
                        <div class="department-card" data-dept="Achat">
                            <h3>Achat</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="Communication">
                            <h3>Communication</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="Centre de traitement des dechets">
                            <h3>Centre de traitement des déchets</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="Magasin">
                            <h3>Magasin</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="QHSE">
                            <h3>QHSE</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="PU">
                            <h3>PU</h3>
                            <p>0 rapport</p>
                        </div>
                        <div class="department-card" data-dept="service juridique">
                            <h3>Service juridique</h3>
                            <p>0 rapport</p>
                        </div>
                    </div>

                    <div class="department-results">
                        <h3 id="dept-title">Rapports du département: <span></span></h3>
                        <table id="dept-results-table">
                            <thead>
                                <tr>
                                    <th>Nom</th>
                                    <th>Prénom</th>
                                    <th>Établissement</th>
                                    <th>Dates</th>
                                    <th>PDF</th>
                                    <th>Appréciation</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Les résultats seront ajoutés dynamiquement -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Rapports Tab -->
                <div id="rapports" class="tab-content">
                    <h2>Tous les Rapports</h2>
                    <div class="sort-options">
                        <label for="sort-by">Trier par:</label>
                        <select id="sort-by">
                            <option value="date-ajout">Date d'ajout</option>
                            <option value="nom">Nom</option>
                            <option value="prenom">Prénom</option>
                            <option value="departement">Département</option>
                            <option value="date-debut">Date de début</option>
                        </select>
                    </div>

                    <table id="all-reports-table">
                        <thead>
                            <tr>
                                <th>Nom</th>
                                <th>Prénom</th>
                                <th>Département</th>
                                <th>Établissement</th>
                                <th>Dates</th>
                                <th>PDF</th>
                                <th>Appréciation</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Les rapports seront ajoutés dynamiquement -->
                        </tbody>
                    </table>
                </div>

                <!-- Utilisateurs Tab -->
                <div id="utilisateurs" class="tab-content">
                    <h2>Gestion des Utilisateurs</h2>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="user-nom">Nom</label>
                            <input type="text" id="user-nom" required>
                        </div>
                        <div class="form-group">
                            <label for="user-prenom">Prénom</label>
                            <input type="text" id="user-prenom" required>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="user-email">Email</label>
                            <input type="email" id="user-email" required>
                        </div>
                        <div class="form-group">
                            <label for="user-role">Rôle</label>
                            <select id="user-role" required>
                                <option value="">Sélectionner un rôle</option>
                                <option value="admin">Administrateur</option>
                                <option value="user">Utilisateur</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="form-buttons">
                        <button id="add-user-btn" class="btn-primary">Ajouter Utilisateur</button>
                    </div>
                    
                    <h3>Liste des Utilisateurs</h3>
                    <table id="users-table">
                        <thead>
                            <tr>
                                <th>Nom</th>
                                <th>Prénom</th>
                                <th>Email</th>
                                <th>Rôle</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Admin</td>
                                <td>System</td>
                                <td>admin@example.com</td>
                                <td>Administrateur</td>
                                <td>
                                    <button class="action-btn edit-btn"><i class="fas fa-edit"></i></button>
                                    <button class="action-btn delete-btn"><i class="fas fa-trash"></i></button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </main>
        </div>
    </div>

    <!-- Modal pour ajouter une appréciation -->
    <div id="appreciation-modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Ajouter une appréciation</h2>
            <textarea id="appreciation-text" placeholder="Saisissez votre appréciation ici..."></textarea>
            <div class="modal-buttons">
                <button id="save-appreciation" class="btn-primary">Enregistrer</button>
                <button id="cancel-appreciation" class="btn-secondary">Annuler</button>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div id="notification" class="notification"></div>

    <script>
        // URL de base de l'API
        const API_BASE_URL = 'http://localhost:3000/api';

        // Données simulées pour les rapports
        let rapports = [
            {
                id: 1,
                nom: "Dupont",
                prenom: "Jean",
                email: "jean.dupont@email.com",
                telephone: "0123456789",
                dateNaissance: "1998-05-15",
                dateDebut: "2023-01-15",
                dateFin: "2023-06-15",
                etablissement: "Université Paris-Saclay",
                departement: "Informatique",
                fichier: "rapport_dupont_jean.pdf",
                dateAjout: "2023-06-20",
                appreciation: ""
            },
            {
                id: 2,
                nom: "Martin",
                prenom: "Sophie",
                email: "sophie.martin@email.com",
                telephone: "0987654321",
                dateNaissance: "1999-08-22",
                dateDebut: "2023-02-01",
                dateFin: "2023-07-01",
                etablissement: "HEC Paris",
                departement: "Marketing",
                fichier: "rapport_martin_sophie.pdf",
                dateAjout: "2023-07-05",
                appreciation: "Excellent travail, très professionnel"
            },
            {
                id: 3,
                nom: "Bernard",
                prenom: "Luc",
                email: "luc.bernard@email.com",
                telephone: "0654321987",
                dateNaissance: "1997-11-10",
                dateDebut: "2023-03-10",
                dateFin: "2023-08-10",
                etablissement: "ESSEC Business School",
                departement: "Ressources Humaines",
                fichier: "rapport_bernard_luc.pdf",
                dateAjout: "2023-08-15",
                appreciation: ""
            }
        ];

        // Éléments DOM
        const tabLinks = document.querySelectorAll('.sidebar li');
        const tabContents = document.querySelectorAll('.tab-content');
        const rapportForm = document.getElementById('rapport-form');
        const searchBtn = document.getElementById('search-btn');
        const departmentCards = document.querySelectorAll('.department-card');
        const sortSelect = document.getElementById('sort-by');
        const modal = document.getElementById('appreciation-modal');
        const closeModal = document.querySelector('.close');
        const saveAppreciationBtn = document.getElementById('save-appreciation');
        const cancelAppreciationBtn = document.getElementById('cancel-appreciation');
        const fileInput = document.getElementById('fichier');
        const fileNameSpan = document.getElementById('file-name');
        const notification = document.getElementById('notification');

        // Variables globales
        let currentReportId = null;

        // Changement d'onglets
        tabLinks.forEach(link => {
            link.addEventListener('click', () => {
                const tabId = link.getAttribute('data-tab');
                
                // Mettre à jour la classe active
                tabLinks.forEach(l => l.classList.remove('active'));
                link.classList.add('active');
                
                // Afficher le contenu correspondant
                tabContents.forEach(content => {
                    content.classList.remove('active');
                    if (content.id === tabId) {
                        content.classList.add('active');
                        
                        // Charger les données si nécessaire
                        if (tabId === 'rapports') {
                            loadAllReports();
                        }
                    }
                });
            });
        });

        // Afficher le nom du fichier sélectionné
        fileInput.addEventListener('change', function() {
            if (this.files.length > 0) {
                fileNameSpan.textContent = this.files[0].name;
            } else {
                fileNameSpan.textContent = '';
            }
        });

        // Soumission du formulaire de nouveau rapport
        rapportForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            // Validation des dates
            const dateDebut = new Date(document.getElementById('date-debut').value);
            const dateFin = new Date(document.getElementById('date-fin').value);
            
            if (dateFin <= dateDebut) {
                showNotification("La date de fin doit être postérieure à la date de début", "error");
                return;
            }
            
            const nouveauRapport = {
                id: rapports.length > 0 ? Math.max(...rapports.map(r => r.id)) + 1 : 1,
                nom: document.getElementById('nom').value,
                prenom: document.getElementById('prenom').value,
                email: document.getElementById('email').value,
                telephone: document.getElementById('telephone').value,
                dateNaissance: document.getElementById('date-naissance').value,
                dateDebut: document.getElementById('date-debut').value,
                dateFin: document.getElementById('date-fin').value,
                etablissement: document.getElementById('etablissement').value,
                departement: document.getElementById('departement').value,
                fichier: document.getElementById('fichier').files[0]?.name || 'fichier.pdf',
                dateAjout: new Date().toISOString().split('T')[0],
                appreciation: ""
            };
            
            rapports.push(nouveauRapport);
            showNotification('Rapport enregistré avec succès!', 'success');
            rapportForm.reset();
            fileNameSpan.textContent = '';
            
            // Mettre à jour les comptes de départements
            updateDepartmentCounts();
        });

        // Recherche de rapports
        searchBtn.addEventListener('click', () => {
            const searchTerm = document.getElementById('search-input').value.toLowerCase();
            const departementFilter = document.getElementById('filter-departement').value;
            const etablissementFilter = document.getElementById('filter-etablissement').value.toLowerCase();
            const dateDebutFilter = document.getElementById('filter-date-debut').value;
            const dateFinFilter = document.getElementById('filter-date-fin').value;
            
            const filteredRapports = rapports.filter(rapport => {
                const matchesSearch = searchTerm === '' || 
                    rapport.nom.toLowerCase().includes(searchTerm) ||
                    rapport.prenom.toLowerCase().includes(searchTerm) ||
                    rapport.etablissement.toLowerCase().includes(searchTerm) ||
                    rapport.departement.toLowerCase().includes(searchTerm);
                    
                const matchesDepartement = departementFilter === '' || rapport.departement === departementFilter;
                const matchesEtablissement = etablissementFilter === '' || rapport.etablissement.toLowerCase().includes(etablissementFilter);
                
                let matchesDate = true;
                if (dateDebutFilter && dateFinFilter) {
                    matchesDate = rapport.dateDebut >= dateDebutFilter && rapport.dateFin <= dateFinFilter;
                } else if (dateDebutFilter) {
                    matchesDate = rapport.dateDebut >= dateDebutFilter;
                } else if (dateFinFilter) {
                    matchesDate = rapport.dateFin <= dateFinFilter;
                }
                
                return matchesSearch && matchesDepartement && matchesEtablissement && matchesDate;
            });
            
            displaySearchResults(filteredRapports);
        });

        // Afficher les résultats de recherche
        function displaySearchResults(results) {
            const tbody = document.querySelector('#results-table tbody');
            tbody.innerHTML = '';
            
            if (results.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="8" style="text-align: center;">Aucun résultat trouvé</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            results.forEach(rapport => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${rapport.nom}</td>
                    <td>${rapport.prenom}</td>
                    <td>${rapport.departement}</td>
                    <td>${rapport.etablissement}</td>
                    <td>${formatDate(rapport.dateDebut)} - ${formatDate(rapport.dateFin)}</td>
                    <td><a href="#" class="view-btn"><i class="fas fa-file-pdf"></i> PDF</a></td>
                    <td>${rapport.appreciation || 'Aucune'}</td>
                    <td>
                        <button class="action-btn view-btn" data-id="${rapport.id}"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn add-appreciation" data-id="${rapport.id}"><i class="fas fa-star"></i></button>
                        <button class="action-btn delete-btn" data-id="${rapport.id}"><i class="fas fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
            
            // Ajouter les écouteurs d'événements pour les boutons
            addActionListeners();
        }

        // Filtrer par département
        departmentCards.forEach(card => {
            card.addEventListener('click', () => {
                const departement = card.getAttribute('data-dept');
                document.querySelector('#dept-title span').textContent = departement;
                
                const filteredRapports = rapports.filter(rapport => rapport.departement === departement);
                displayDepartmentResults(filteredRapports);
            });
        });

        // Afficher les résultats par département
        function displayDepartmentResults(results) {
            const tbody = document.querySelector('#dept-results-table tbody');
            tbody.innerHTML = '';
            
            if (results.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="7" style="text-align: center;">Aucun rapport pour ce département</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            results.forEach(rapport => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${rapport.nom}</td>
                    <td>${rapport.prenom}</td>
                    <td>${rapport.etablissement}</td>
                    <td>${formatDate(rapport.dateDebut)} - ${formatDate(rapport.dateFin)}</td>
                    <td><a href="#" class="view-btn"><i class="fas fa-file-pdf"></i> PDF</a></td>
                    <td>${rapport.appreciation || 'Aucune'}</td>
                    <td>
                        <button class="action-btn view-btn" data-id="${rapport.id}"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn add-appreciation" data-id="${rapport.id}"><i class="fas fa-star"></i></button>
                        <button class="action-btn delete-btn" data-id="${rapport.id}"><i class="fas fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
            
            // Ajouter les écouteurs d'événements pour les boutons
            addActionListeners();
        }

        // Charger tous les rapports
        function loadAllReports() {
            const tbody = document.querySelector('#all-reports-table tbody');
            tbody.innerHTML = '';
            
            if (rapports.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="8" style="text-align: center;">Aucun rapport enregistré</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            // Trier les rapports selon la sélection
            const sortBy = sortSelect.value;
            let sortedRapports = [...rapports];
            
            switch(sortBy) {
                case 'nom':
                    sortedRapports.sort((a, b) => a.nom.localeCompare(b.nom));
                    break;
                case 'prenom':
                    sortedRapports.sort((a, b) => a.prenom.localeCompare(b.prenom));
                    break;
                case 'departement':
                    sortedRapports.sort((a, b) => a.departement.localeCompare(b.departement));
                    break;
                case 'date-debut':
                    sortedRapports.sort((a, b) => new Date(a.dateDebut) - new Date(b.dateDebut));
                    break;
                default: // date-ajout
                    sortedRapports.sort((a, b) => new Date(b.dateAjout) - new Date(a.dateAjout));
            }
            
            sortedRapports.forEach(rapport => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${rapport.nom}</td>
                    <td>${rapport.prenom}</td>
                    <td>${rapport.departement}</td>
                    <td>${rapport.etablissement}</td>
                    <td>${formatDate(rapport.dateDebut)} - ${formatDate(rapport.dateFin)}</td>
                    <td><a href="#" class="view-btn"><i class="fas fa-file-pdf"></i> PDF</a></td>
                    <td>${rapport.appreciation || 'Aucune'}</td>
                    <td>
                        <button class="action-btn view-btn" data-id="${rapport.id}"><i class="fas fa-eye"></i></button>
                        <button class="action-btn edit-btn add-appreciation" data-id="${rapport.id}"><i class="fas fa-star"></i></button>
                        <button class="action-btn delete-btn" data-id="${rapport.id}"><i class="fas fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
            
            // Ajouter les écouteurs d'événements pour les boutons
            addActionListeners();
        }

        // Trier les rapports
        sortSelect.addEventListener('change', loadAllReports);

        // Mettre à jour les comptes de départements
        function updateDepartmentCounts() {
            departmentCards.forEach(card => {
                const dept = card.getAttribute('data-dept');
                const count = rapports.filter(r => r.departement === dept).length;
                card.querySelector('p').textContent = `${count} rapport${count !== 1 ? 's' : ''}`;
            });
        }

        // Ajouter des écouteurs d'événements pour les boutons d'action
        function addActionListeners() {
            // Boutons pour ajouter une appréciation
            document.querySelectorAll('.add-appreciation').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const reportId = parseInt(e.currentTarget.getAttribute('data-id'));
                    openAppreciationModal(reportId);
                });
            });
            
            // Boutons de suppression
            document.querySelectorAll('.delete-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const reportId = parseInt(e.currentTarget.getAttribute('data-id'));
                    if (confirm('Êtes-vous sûr de vouloir supprimer ce rapport ?')) {
                        deleteReport(reportId);
                    }
                });
            });

            // Boutons de visualisation
            document.querySelectorAll('.view-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.preventDefault();
                    const reportId = parseInt(e.currentTarget.getAttribute('data-id'));
                    const rapport = rapports.find(r => r.id === reportId);
                    if (rapport && rapport.fichier) {
                        // Simuler l'ouverture du PDF (dans une vraie application, on ouvrirait le fichier)
                        alert(`Ouverture du fichier: ${rapport.fichier}`);
                    }
                });
            });
        }

        // Ouvrir la modal d'appréciation
        function openAppreciationModal(reportId) {
            currentReportId = reportId;
            const rapport = rapports.find(r => r.id === reportId);
            document.getElementById('appreciation-text').value = rapport.appreciation || '';
            modal.style.display = 'block';
        }

        // Fermer la modal d'appréciation
        closeModal.addEventListener('click', () => {
            modal.style.display = 'none';
        });

        cancelAppreciationBtn.addEventListener('click', () => {
            modal.style.display = 'none';
        });

        // Enregistrer l'appréciation
        saveAppreciationBtn.addEventListener('click', () => {
            const appreciation = document.getElementById('appreciation-text').value;
            const rapportIndex = rapports.findIndex(r => r.id === currentReportId);
            
            if (rapportIndex !== -1) {
                rapports[rapportIndex].appreciation = appreciation;
                showNotification('Appréciation enregistrée avec succès!', 'success');
                modal.style.display = 'none';
                
                // Recharger les données affichées
                if (document.getElementById('recherche').classList.contains('active')) {
                    searchBtn.click();
                } else if (document.getElementById('rapports').classList.contains('active')) {
                    loadAllReports();
                }
            }
        });

        // Supprimer un rapport
        function deleteReport(reportId) {
            rapports = rapports.filter(r => r.id !== reportId);
            showNotification('Rapport supprimé avec succès!', 'success');
            
            // Recharger les données affichées
            if (document.getElementById('recherche').classList.contains('active')) {
                searchBtn.click();
            } else if (document.getElementById('rapports').classList.contains('active')) {
                loadAllReports();
            }
            
            updateDepartmentCounts();
        }

        // Formater une date au format JJ/MM/AAAA
        function formatDate(dateString) {
            if (!dateString) return 'N/A';
            const date = new Date(dateString);
            return `${date.getDate().toString().padStart(2, '0')}/${(date.getMonth() + 1).toString().padStart(2, '0')}/${date.getFullYear()}`;
        }

        // Afficher une notification
        function showNotification(message, type) {
            notification.textContent = message;
            notification.className = `notification ${type}`;
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Fermer la modal si on clique en dehors
        window.addEventListener('click', (e) => {
            if (e.target === modal) {
                modal.style.display = 'none';
            }
        });

        // Initialisation
        document.addEventListener('DOMContentLoaded', () => {
            updateDepartmentCounts();
            loadAllReports();
            
            // Ajouter des gestionnaires d'événements pour les boutons d'en-tête
            document.getElementById('logout-btn').addEventListener('click', () => {
                if (confirm('Êtes-vous sûr de vouloir vous déconnecter ?')) {
                    showNotification('Déconnexion réussie', 'success');
                    // Redirection vers la page de connexion dans une vraie application
                }
            });
            
            document.getElementById('profile-btn').addEventListener('click', () => {
                alert('Gestion du profil - À implémenter');
            });
            
            document.getElementById('settings-btn').addEventListener('click', () => {
                alert('Paramètres - À implémenter');
            });
        });
    </script>
</body>
</html>
