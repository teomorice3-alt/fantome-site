# Fantôme — site à déployer

Site statique : rien à installer, rien à compiler. Un serveur qui sert
des fichiers suffit.

```
index.html          la page (80 Ko)
images/             les six photos (1 Mo)
favicon.svg         l'icône d'onglet
```

## Mettre en ligne sur Vercel

1. Crée un compte sur vercel.com **à ton vrai nom** : en tant que
   particulier tu peux rester anonyme sur le site, à condition que
   l'hébergeur détienne ton identité.
2. Nouveau projet → dépose ce dossier entier (ou relie un dépôt GitHub
   qui le contient). Aucun réglage de build : c'est du HTML statique.
3. Vercel te donne une adresse en `.vercel.app`. Tu pourras y brancher
   un nom de domaine plus tard.

Netlify, Cloudflare Pages, GitHub Pages ou un hébergeur français
(o2switch, Infomaniak, OVH) fonctionnent exactement pareil.

**Attention** : l'offre gratuite de Vercel est réservée aux projets non
commerciaux. Tant que le site est une vitrine, c'est bon. Le jour où tu
vends, relis leurs conditions.

## Les trois réglages, en haut du `<script>` de `index.html`

```js
var BOUTIQUE_OUVERTE = false;   // true = le panier et les CGV s'ouvrent
var EMAIL_BOUTIQUE = "commandes@fantome.example";   // ← ton adresse
var LIVRAISON = { prix: null, offertDes: null, delai: "" };
```

- **`EMAIL_BOUTIQUE`** : à changer en premier. Sans elle, la liste
  d'attente et les commandes n'arrivent nulle part.
- **`LIVRAISON`** : tant que `prix` vaut `null`, la page annonce que le
  port sera calculé à la commande. Renseigne `prix` (en euros),
  `offertDes` (le montant à partir duquel il est offert, ou `null`) et
  `delai` (ex. `"3 à 5 jours ouvrés"`).
- **`BOUTIQUE_OUVERTE`** : à passer à `true` seulement une fois ton
  activité déclarée et les mentions légales complétées.

Les prix sont juste au-dessus, dans `PRIX`.

## Avant d'ouvrir la boutique

1. Déclarer l'activité (micro-entrepreneur, gratuit, en ligne sur
   formalites.entreprises.gouv.fr). L'achat-revente exige une
   immatriculation.
2. Compléter les champs surlignés en champagne dans la section
   « Informations légales » — ils apparaissent en cherchant `aremplir`
   dans le fichier.
3. Faire relire les CGV par un professionnel.
4. Renseigner les frais de port.
5. Passer `BOUTIQUE_OUVERTE` à `true`.

## Ce qui n'est pas branché

Le tunnel de commande et la liste d'attente ouvrent la messagerie du
visiteur avec un message prêt à envoyer. **Rien n'est enregistré côté
serveur** : si le visiteur ferme l'onglet sans envoyer, c'est perdu.
Pour un vrai enregistrement, remplace le corps de la fonction
`envoyerCommande(cmd)` — l'exemple `fetch` est en commentaire juste
au-dessus. Le formulaire de newsletter, lui, n'envoie rien du tout.

La 3D du stylo charge Three.js depuis un CDN : sans connexion, une
photo détourée s'affiche à la place et le reste de la page fonctionne.
