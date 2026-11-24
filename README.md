# AelySafe — Web app V0

Prototype cliquable de l'application de sécurité personnelle AelySafe (Challenge Start'Up MCD, MBway — pilote Toulouse).

## Fonctionnalités de la V0
- Inscription réservée aux 18 ans et plus, vérification pièce d'identité + selfie en direct (simulée)
- Ouvert aux femmes et aux hommes majeurs, sans marrainage
- Protection de la communauté : signalement d'un utilisateur, suspension immédiate, bannissement définitif lié à l'empreinte de la pièce d'identité (démo du refus : nom de famille `Test-Banni`)
- Piste à valider : contrôle des antécédents d'agression avec les autorités (fichiers réservés aux organismes autorisés par la loi)
- Bouton SOS à appui long (2 s), appui bracelet / montre / porte-clés simulé, alerte silencieuse, annulation par code PIN
- Vraie carte de Toulouse (OpenStreetMap), aux couleurs AelySafe, jour et nuit : lieux de sûreté réels (pharmacies, police, hôpitaux, gares) + partenaires, lignes de métro et tram, carte de chaleur des signalements (simulée), itinéraire à pied avec recherche d'adresse
- Mode aidant : réception d'alerte à proximité, charte d'intervention non violente
- Proches de confiance
- Freemium : app gratuite avec montre connectée, bracelet / porte-clés à acheter
- Séparation données personnelles / signalements anonymes (zone ~500 m, tranche horaire, contexte) pour la smart city

Tout tourne dans le navigateur (localStorage), aucun serveur. Ouvrir `index.html` suffit.

## Carte : 100 % gratuit, sans clé API
| Rôle | Service | Coût |
|---|---|---|
| Affichage | MapLibre GL JS 4.7.1 (copié dans `vendor/`) | gratuit, open source |
| Fond de carte | OpenFreeMap (`tiles.openfreemap.org`) | gratuit, sans clé ni limite |
| Lieux de sûreté, métro et tram | Overpass API (OpenStreetMap), mis en cache 24 h | gratuit, usage raisonnable |
| Recherche d'adresse | Photon (`photon.komoot.io`) | gratuit, usage raisonnable |
| Itinéraire à pied | OSRM FOSSGIS (`routing.openstreetmap.de`) | gratuit, usage raisonnable |

Personnaliser : couleurs dans la constante `PAL` de `index.html` (jour / nuit).
Ajouter des partenaires : éditer `partenaires.json` (nom, lat, lon, horaires).
Hors ligne ou dans l'aperçu Claude, l'app affiche un plan simplifié à la place.

Pour un vrai lancement, prévoir d'héberger soi-même la recherche et l'itinéraire (Photon, OSRM ou Valhalla sur un petit serveur) : les services publics gratuits ne garantissent pas la disponibilité.

## Mise en ligne via GitHub Pages
Settings → Pages → Source : `Deploy from a branch` → branche `main`, dossier `/ (root)`.
Le site sera disponible sur `https://<utilisateur>.github.io/<depot>/`.

En cas de danger réel : 17, 112, ou 114 par SMS.
