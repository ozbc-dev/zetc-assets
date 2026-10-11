# SIGNATURES MAIL — ÉTAT DU CHANTIER

Version : 1.0 — 2026-10-11
Dépôt : `ozbc-dev/zetc-assets` (ce fichier + images hébergées)
Périmètre : signatures Gmail des 4 boîtes Google Workspace zetc.fr et de leurs alias d'émission ; hébergement des images ; authentification DNS des six domaines d'émission.
Arbitre : Olivier Zebic. Exécutant : Claude (projet « Sites & Shopify »).

---

## 1. DOCTRINE (arbitrages clos — ne pas rouvrir)

| # | Arbitrage | Décision | Date |
|---|---|---|---|
| D1 | Outil | **Sign.UseWise** (Miadria, HR). Écriture directe dans Gmail par l'API, aucun serveur intermédiaire, facturation **par compte Google Workspace** (alias gratuits), 210 $/an jusqu'à 30 comptes. Signitic résilié (facturation à l'adresse → 20 licences pour 4 boîtes), désinstallé du Workspace, suppression du compte demandée. Exclaimer écarté (alias uniquement en server-side), SyncSignature écarté (alias = siège). | 2026-10-11 |
| D2 | Design | Système des **cartes de visite 2026 « Bâtisseurs de vignobles »** : bandeau = bloc du recto (tuiles Z&C, CARRÉ BLEU, Renouvellement du vignoble, rendu vectoriel) + tagline au pluriel ; identité en texte avec filet or ; légende = motifs du verso, sur trois lignes, libellés en sans gras ; ligne de pied « Pionnier et leader de l'irrigation goutte-à-goutte des plantiers en appellation ». | 2026-10-11 |
| D3 | Domaines → entité | zetc.fr, carreb.com, carre-bleu.eu, xvigne.fr → Bâtisseurs (CARRÉ BLEU + Z&C). elde.company → ELDE (logo oiseau orange sur tuile crème). wino.company → WINO (logo prune sur tuile crème). Holdings : sans tagline, sans légende, sans ligne de pied. | 2026-10-11 |
| D4 | Adresses affichées | Adresses **courtes**, ordre de la carte : `prenom-court@carreb.com · prenom-court@zetc.fr` (oz, jc, ld). carre-bleu.eu jamais affichée (domaine en extinction). Adresses de rôle : leur seule adresse. | 2026-10-11 |
| D5 | Olivier | Nom seul, **sans fonction** dans toutes ses signatures (gabarit dédié ; le champ Fonction de l'annuaire Google n'a pas été touché). | 2026-10-11 |
| D6 | Hébergement images | `assets.zetc.fr` (Vercel, projet `zetc-assets` lié au dépôt GitHub, CNAME OVH). Jamais Shopify (domaine d'une seule marque), jamais Drive, jamais l'hébergement de l'éditeur. Cache un an immuable → **tout changement d'image = nouveau nom de fichier**. | 2026-10-11 |
| D7 | Alias d'émission | Toutes les formes utiles existent en « Envoyer en tant que » (créées dans Gmail par chaque utilisateur, pas par l'outil — voir bug B1). Forme `olivier@`/`jerome@`/`ludivine@` non créée (non retenue à ce stade). | 2026-10-11 |
| D8 | Mobile | Pas de signature HTML automatique sur l'app Gmail (limite Google). Add-on Sign.UseWise installé au niveau du domaine pour insertion manuelle par alias. | 2026-10-11 |

---

## 2. ARCHITECTURE EN PLACE

### 2.1 Sign.UseWise (sign.usewise.app, admin olivier.zebic@zetc.fr)
- Délégation à l'échelle du domaine active, compte de service `signusewiseapp@…gserviceaccount.com`.
- **Companies** : `Default` (= Bâtisseurs ; domaines zetc.fr, xvigne.fr, carre-bleu.eu, carreb.com ; logo `bandeau-batisseurs-v2@2x.png`) · `ELDE` (elde.company ; `tuile-elde@2x.png`) · `WINO` (wino.company ; `tuile-wino@2x.png`). Le logo d'entité est résolu par le **domaine de l'adresse d'émission** via `{companyLogo}`.
- **Templates** (sources HTML dans `signatures-usewise/` de ce dépôt) :
  - `Batisseurs - Olivier` · `Batisseurs - Jerome` · `Batisseurs - Ludivine` (deux adresses en dur par personne)
  - `Batisseurs - Roles (contact@)` (nom « CARRÉ BLEU », `{email}`)
  - `Holding (ELDE - WINO)` (logo 300 px, nom, fonction si renseignée, mobile, `{email}`)
  - `Default` (modèle d'origine de l'outil, inutilisé)
- **Scheduling** : synchronisation Google 05:30, réapplication des signatures 06:00 (Europe/Paris) — indispensable aux campagnes.
- **Marketing** : aucune campagne créée à ce jour.

### 2.2 Affectations (31 adresses, 29 signées) — état au 2026-10-11
| Boîte | Adresses | Gabarit |
|---|---|---|
| olivier.zebic@zetc.fr | zetc.fr, carreb.com, carre-bleu.eu, oz@carreb.com, oz@zetc.fr | Batisseurs - Olivier |
| | elde.company, wino.company | Holding |
| jerome.courgey@zetc.fr | zetc.fr, carreb.com, carre-bleu.eu, jc@carreb.com, jc@zetc.fr | Batisseurs - Jerome |
| | wino.company | Holding |
| ludivine.delaeter@zetc.fr | zetc.fr, carreb.com, carre-bleu.eu, ld@carreb.com, ld@zetc.fr | Batisseurs - Ludivine |
| | elde.company, wino.company | Holding |
| contact@zetc.fr | contact@zetc.fr, contact@carre-bleu.eu, carreb.com : contact, commercial, direction, communication, technique, office, marketing | Batisseurs - Roles |
| | contact@wino.company, direction@wino.company | **aucune** (voir P1) |

### 2.3 Images (assets.zetc.fr/signatures/)
`bandeau-batisseurs-v2` (560×140) · `bandeau-batisseurs` (v1 560×110, obsolète, conservée pour le cache) · `tuile-elde`, `tuile-wino` (300×110) · `legende-zc`, `legende-carre-bleu`, `legende-renouvellement` (44×24) — chacune en 1x et @2x.
Sources de fabrication : SVG recto/verso des cartes 2026 (Drive COMMUNICATION / 02_IMPRIMES / CARTES-DE-VISITE / 2026_Bâtisseur-de-vignobles), kits logos ELDE et WINO du 2026-10-08.

### 2.4 DNS (zones OVH) — authentification, état au 2026-10-11
| Domaine | SPF (TXT) | DKIM `google._domainkey` | DMARC |
|---|---|---|---|
| zetc.fr | OVH + Zoho + Books + Google + ZeptoMail + Campaigns, ~all | publié, auth. lancée | p=none, rua olivier.zebic@zetc.fr |
| carreb.com | Google, ~all | publié, auth. lancée | p=none, rua contact@carreb.com |
| carre-bleu.eu | Google + Books + Campaigns, ~all | publié, auth. lancée | p=none |
| wino.company | Google, ~all | publié, auth. lancée | p=none, rua olivier.zebic@wino.company |
| elde.company | Google, ~all | publié, auth. lancée | p=none, rua olivier.zebic@elde.company |
| xvigne.fr | Google, ~all ; MX Google complétés | publié, auth. lancée | p=none, rua olivier.zebic@xvigne.fr |
Supprimés : enregistrements de type « SPF » (déprécié, doublon invalidant), traces Brevo (code, clé `mail._domainkey`, DMARC) sur zetc.fr et carre-bleu.eu.

---

## 3. PROCÉDURES

**Lancer une campagne de bannière** : Marketing → nouvelle campagne (nom, début, fin, HTML : image 560×64 hébergée sur assets.zetc.fr + lien avec UTM) → la réapplication de 06:00 la propage ; « Reapply » sur les adresses pour une mise en ligne immédiate. Déposer d'abord l'image dans ce dépôt (`signatures/campagnes/…`), nom de fichier unique.

**Modifier un gabarit** : Templates → sélectionner → Source → coller le HTML → Save → Users → sélectionner les adresses → Reapply. Mettre à jour la source dans `signatures-usewise/`.

**Nouvel alias d'émission** : l'utilisateur l'ajoute dans Gmail (Paramètres → Comptes → Envoyer en tant que, « traiter comme un alias ») → Sign.UseWise : Refresh → affecter le gabarit à la nouvelle ligne.

**Nouvelle personne** : compte Workspace + alias → Refresh → créer son gabarit « Batisseurs - Prénom » (copie, deux adresses en dur) → affecter.

---

## 4. POINTS OUVERTS (questions fermées, recommandation)

| # | Question | Reco |
|---|---|---|
| P1 | Gabarit « Rôles WINO » pour contact@/direction@wino.company (tuile WINO + « WINO » + adresse) ? | Oui, 5 min |
| P2 | Passer DMARC en `p=quarantine` sur les six domaines une fois les six authentifications DKIM confirmées et des rapports reçus (1–2 semaines) ? | Oui |
| P3 | Supprimer les deux CNAME DKIM OVH Mail sur carre-bleu.eu (plus d'envoi par OVH) ? | Oui |
| P4 | Souscription Sign.UseWise annuelle (210 $) avant fin d'essai (≈ 2026-10-21) ? | Oui |
| P5 | Statut de l'alias olivier.zebic@gmail.com (ni signature ni authentification possibles) : conserver en réception seule ? | Oui, conserver |
| P6 | Refaire proprement la tagline « Bâtisseurs » (pluriel composé à partir du fichier d'impression) avec la police source quand elle sera identifiée ? | Oui, basse priorité |

---

## 5. BUGS SIGN.USEWISE RENCONTRÉS (à signaler au support)
- **B1** Users → « Create new sendAs » : l'alias sélectionné dans la liste est ignoré, la création utilise toujours le premier alias de la liste (3 essais, 3 méthodes). Contournement : création dans Gmail par l'utilisateur.
- **B2** Users → « Assign » groupé : échec HTTP 400 sur une boîte (Ludivine) alors que l'affectation adresse par adresse réussit. Reapply groupé fonctionne.
- **B3** Companies : retirer un domaine d'un profil ne le réattribue pas au profil d'origine ; il devient orphelin et les adresses retombent sur `Default` sans avertissement.
- Cosmétique : l'éditeur et la prévisualisation bloquent les images externes (CSP) ; le rendu réel dans Gmail est correct.

---

## 6. JOURNAL
- 2026-10-06 — Résiliation Signitic ; comparatif outils ; inventaire sendAs (19 adresses sur 3 boîtes, signatures Signitic déjà cassées).
- 2026-10-08 — Essai Sign.UseWise ; logos ELDE/WINO finalisés ; aperçus v1→v4.
- 2026-10-11 — Aperçu v5 validé ; dépôt zetc-assets + Vercel + CNAME ; profils Companies ; 6 gabarits ; Scheduling ; alias créés par les 3 utilisateurs (31 adresses) ; 29 affectations ; correction profil ELDE orphelin ; bandeau v2 (140 px) ; légende en lignes ; adresses courtes ; Signitic désinstallé ; SPF/DMARC/MX corrigés, 6 clés DKIM publiées et vérifiées, Brevo retiré.
