# AelySafe — Web app V0

Aux couleurs de la charte graphique AelySafe : crème, rose framboise, orange, mauve, bleu ciel, prune ; titres en Antipasto, texte en Satoshi (polices et logo dans `assets/`).

Prototype cliquable de l'application de sécurité personnelle AelySafe (Challenge Start'Up MCD, MBway — pilote Toulouse).

## Fonctionnalités de la V0
- Inscription réservée aux 18 ans et plus, vérification pièce d'identité + selfie en direct (simulée)
- Ouvert aux femmes et aux hommes majeurs, sans marrainage
- Protection de la communauté : signalement d'un utilisateur, suspension immédiate, bannissement définitif lié à l'empreinte de la pièce d'identité (démo du refus : nom de famille `Test-Banni`)
- Piste à valider : contrôle des antécédents d'agression avec les autorités (fichiers réservés aux organismes autorisés par la loi)
- Bouton SOS : un appui lance l'alerte immédiatement (bracelet / montre / porte-clés simulés), alerte silencieuse, annulation par code PIN
- Enregistrement audio automatique pendant toute l'alerte (micro du téléphone) : réécoute et téléchargement dès la fin de l'alerte, puis dans Compte ; suppression seulement après confirmation et code PIN
- Réseau d'entraide en temps réel entre téléphones : l'aidant reçoit l'alerte (vibration + notification) ; quand il accepte, la personne en danger reçoit une vibration et une notification « Quelqu'un vient vous aider »
- Installable sur l'écran d'accueil (PWA)
- Autorisations micro et notifications demandées par le téléphone lui-même (fenêtres du système) dès l'ouverture ; réglages dans Compte
- Bouton en haut à droite selon l'onglet : Appairer (Accueil), Charte d'entraide (Aider), + Ajouter (Réseau), Mes données (Compte)
- Proches de confiance : bouton Modifier, retrait seulement depuis la fiche avec double confirmation
- Carte plein écran façon Plans (Apple) : panneau de recherche en bas, boutons flottants (SOS, calques, lampadaires, me localiser)
- Lampadaires : bouton pour demander un éclairage renforcé dans un rayon de 200 m pendant 15 min (simulation smart city, points lumineux réels de la Ville de Toulouse ou d'OpenStreetMap)
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
| Lignes et arrêts métro, tram, téléphérique, Linéo, bus | Tisséo via Open Data Toulouse Métropole (jeux `ligne` et `arret_physique`, ODbL) | gratuit |
| Lampadaires (points lumineux) | Open Data Ville de Toulouse (`points-lumineux`), sinon OpenStreetMap (`highway=street_lamp`) | gratuit |
| Commissariats de police | Open Data Haute-Garonne (`commissariats-de-police-haute-garonne`) | gratuit |
| Pharmacies, hôpitaux, gendarmeries, gares (+ secours si Tisséo indisponible) | Overpass API (OpenStreetMap) | gratuit, usage raisonnable |
| Alertes en temps réel entre téléphones | ntfy.sh (sans compte) | gratuit |
| Recherche d'adresse | Photon (`photon.komoot.io`) | gratuit, usage raisonnable |
| Itinéraire à pied | OSRM FOSSGIS (`routing.openstreetmap.de`) | gratuit, usage raisonnable |

Personnaliser : couleurs dans la constante `PAL` de `index.html` (jour / nuit).
Ajouter des partenaires : éditer `partenaires.json` (nom, lat, lon, horaires).
Les sources officielles priment : un lieu OpenStreetMap en double (même type à moins de 80 m) est écarté. Toutes les données sont mises en cache 24 h sur le téléphone.
Hors ligne ou dans l'aperçu Claude, l'app affiche un plan simplifié à la place.

Pour un vrai lancement, prévoir d'héberger soi-même la recherche et l'itinéraire (Photon, OSRM ou Valhalla sur un petit serveur) : les services publics gratuits ne garantissent pas la disponibilité.

## Tester l'entraide avec deux téléphones
1. Ouvrir le site sur deux téléphones, créer un compte sur chacun, autoriser les notifications.
2. Téléphone B : onglet Aider, cocher « Je suis disponible pour aider ».
3. Téléphone A : appuyer sur SOS (autoriser le micro).
4. B reçoit l'alerte, accepte la charte, « J'y vais » : A vibre et reçoit la notification.

Limites : la vibration n'existe pas sur iPhone (Safari) ; sur iPhone, les notifications web ne marchent qu'après « Ajouter à l'écran d'accueil ». Le canal ntfy.sh est public (nom de canal aléatoire) : suffisant pour une démo, à remplacer par un serveur à vous (ntfy auto-hébergé ou Supabase Realtime) avant un vrai lancement. Les enregistrements audio restent sur le téléphone dans la V0.

## Mise en ligne via GitHub Pages
Settings → Pages → Source : `Deploy from a branch` → branche `main`, dossier `/ (root)`.
Le site sera disponible sur `https://<utilisateur>.github.io/<depot>/`.

En cas de danger réel : 17, 112, ou 114 par SMS.
