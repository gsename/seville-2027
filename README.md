# Séville 2027

Organisation du voyage à 4 : programme jour par jour, vols, logement, activités, budget et remboursements.
Page statique (GitHub Pages), sans serveur ni compte à créer pour les amis.

## Mise en ligne (10 min, une seule fois)

1. **Créer un repo public** sur GitHub, par ex. `seville-2027`, et y déposer tous les fichiers de ce dossier (y compris `.nojekyll`).
2. **Activer Pages** : *Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save*.
   L'app est en ligne sur `https://<ton-compte>.github.io/seville-2027/` après une minute.
3. **Créer la clé d'édition** : *Settings (de ton profil) → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token*
   - Repository access : *Only select repositories* → `seville-2027` uniquement
   - Permissions : *Contents* → *Read and write* (rien d'autre)
   - Expiration : après le voyage (ex. 1er mars 2027)
4. **Ouvrir l'app**, *Réglages* → coller la clé → *Utiliser*. Puis choisir un **code privé** → *Activer*.
5. *Réglages → Copier le lien d'édition* et l'envoyer aux 3 autres (WhatsApp, etc.). En l'ouvrant, leur téléphone garde la clé et le code ; l'app leur demande leur prénom.

L'adresse simple (sans `#cle=…`) est en lecture seule : elle peut circuler librement.

## Comment ça marche

- **Données** : un fichier `trip.json` sur la branche `data` du repo, créée automatiquement à la première modification. Chaque modification est un commit signé du prénom de l'auteur : l'historique sert de journal et de retour arrière.
- **Branche séparée** : les modifications ne relancent pas la publication de la page.
- **Modifs simultanées** : si deux personnes enregistrent en même temps, la seconde est rejouée sur la version à jour, rien n'est écrasé (sauf si les deux modifient la même fiche : la dernière gagne).
- **Mise à jour** : les éditeurs récupèrent les changements des autres toutes les 45 s, les lecteurs toutes les 3 min (et à chaque retour sur l'onglet).
- **Tickets de caisse** : *Budget → Scanner un ticket*. Le texte est lu sur le téléphone (Tesseract.js, téléchargé au premier scan) ; un écran liste ensuite chaque article avec son prix, à vérifier. Chaque ligne est pour « Tous » ou pour une ou plusieurs personnes, et le budget répartit ligne par ligne. La photo n'est pas conservée.
- **Animations** : à l'ouverture, on entre dans les arènes (toucher pour passer). Ensuite, régulièrement, une petite scène traverse le bas de l'écran : bailaoras qui dansent, torero qui fait passer le taureau sous sa muleta (deux passes puis ¡Olé!), tapeo avec le camarero et son plateau, poursuite des danseuses par le taureau, taureau qui percute le bord de l'écran (la page tremble), torero renversé qui perd sa muleta. Sur ordinateur, le curseur devient une muleta : quand le taureau passe, il la suit et chaque passe compte un ¡Olé!. Désactivables par appareil dans *Réglages → Toi* (coupées d'office si le téléphone demande moins d'animations).
- **Météo** : prévisions Open-Meteo (gratuit, sans compte) sur chaque jour du programme, dès 15 jours avant le départ.
- **Aujourd'hui** : pendant le voyage, en haut du programme, le prochain rendez-vous avec compte à rebours, itinéraire Google Maps et logement du soir. Pour le prévisualiser : ajouter `?maintenant=2027-02-12T09:30` à l'adresse.
- **Carte** (onglet) : tous les lieux (activités par jour, idées, logement, aéroport) sur OpenStreetMap. Les lieux sont cherchés autour de la ville du voyage.
- **Idées** : chacun met un pouce, les plus votées remontent.
- **Valise** (onglet) : liste personnelle à cocher (passeport ET carte d'identité pour César, l'un ou l'autre pour les autres), progression de chacun, objets à partager avec qui les apporte.
- **Question du jour** et **La Liga** : une question sur Séville par jour (onglet Fiesta), et un classement général qui sort sur le côté de l'écran à l'ouverture et quand il change.
- **Fiesta** (onglet) : jeux *Toréer* (muleta au doigt ou à la souris), *Attrape la tapa* et *Castañuelas* (sons synthétisés), podium « Mejor torero » et classements. Un taureau se cache derrière une carte du site : le premier qui le touche gagne un ¡Olé! vu par tout le groupe, puis il se recache ailleurs 4 h plus tard. Secrets : secouer le téléphone (le taureau charge), taper « olé » ou toucher trois fois le titre (fiesta), régler un point de « Reste à caler » (tour d'honneur, grande parade quand tout est calé). Les records et les trouvailles sont enregistrés dans `trip.json` (champ `jeux`) avec le prénom ; sans lien d'édition, le record reste sur l'appareil.
- **Hors ligne** : la dernière version reste consultable ; ajoute la page à l'écran d'accueil pour l'avoir comme une app.

## Sécurité

- Tout le contenu du repo est **public** (noms, programme, prix).
- Les champs **Infos privées** (réf. de réservation, code de la porte…) sont chiffrés dans le navigateur (AES-GCM, clé dérivée du code privé). Sans le code, ils sont illisibles, y compris dans le repo. Une réf. de réservation + un nom suffisent souvent à annuler un vol : ne les mets que dans ce champ.
- La clé d'édition ne donne accès qu'à ce repo, en écriture sur les fichiers. Si le lien d'édition fuit : supprime le token sur GitHub, crée-en un nouveau, renvoie un lien.

## Personnaliser

- Prénoms, photos de profil, destination et dates : *Réglages* dans l'app (toucher le rond d'un voyageur pour choisir sa photo). Les photos sont réduites à 480 px et enregistrées dans `trip.json`, donc publiques comme le reste.
- Domaine personnalisé : renseigner `owner` et `repo` dans `window.TRIP_CONFIG` en haut de `index.html`.
- Ouvert en local (hors github.io), l'app passe en mode local : les données restent dans le navigateur.
