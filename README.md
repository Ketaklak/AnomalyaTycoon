# 🌱 Eco-Tycoon – README

## 📌 Objectif

Création d’un **tycoon industriel/écologique** dans Roblox Studio :

- Chaque joueur possède un **Tycoon** (zone).
- Des **droppers** produisent des “ores” (pièces) sur un **conveyor**.
- Les pièces sont détruites dans une **caisse collectrice** (“CollectorHitbox”).
- Le joueur gagne du cash selon un mode choisi :
  - `loop` → paiement automatique à chaque tick.
  - `collect` → paiement uniquement quand l’ore atteint la caisse.

Le jeu inclut déjà une logique d’**écosystème** (météo, pollution) via `EnvironmentService`.

---

## 📁 Scripts & Services

| Script | Rôle |
|--------|------|
| `BuildService` | Gère le **lock/unlock visuel** des items (hologrammes). |
| `Purchase.server.lua` | Gère l’achat d’items via `ProximityPrompt` (paiement, déblocage). |
| `DropperSystem.server.lua` | Spawn des ores, paiement, destruction dans la caisse. |
| `EnvironmentService` | Fournit le facteur d’efficacité (`GetZoneEfficiency`). |

---

## 🛠️ Fonctionnement général

1. **Player Claim / Achat**  
   - Le joueur achète un item via un bouton (`ProximityPrompt`).  
   - `Purchase` débite le cash, appelle `BuildService.Unlock(item)`.

2. **Déverrouillage**  
   - `BuildService` affiche un effet hologramme, puis révèle le modèle réel.

3. **Production**  
   - `DropperSystem` détecte les droppers `Unlocked`.  
   - Chaque dropper démarre une boucle → paiement + `spawnPhysicalOre`.

4. **Transport & Collecte**  
   - Les ores glissent sur le convoyeur.  
   - La `CollectorHitbox` supprime l’ore.  
   - Si `PayOnCollect` est vrai, elle crédite le joueur.

---

## ⚙️ Attributs des droppers

| Nom | Type | Valeur par défaut | Description |
|-----|------|------------------|-------------|
| `Purchasable` | Bool | true | Permet l’achat (géré par `Purchase`). |
| `Unlocked` | Bool | false | Débloqué ou non. |
| `OwnerUserId` | Number | 0 | Défini lors du claim. |
| `PayoutMode` | String | `"loop"` | `"loop"` = paie par tick, `"collect"` = paie en caisse. |
| `OreValue` | Number | 1 | Montant de cash par tick / collecte. |
| `BaseInterval` | Number | 2 | Délai (sec) entre ticks. |
| `MaxOres` | Number | 12 | Nb max d’ores visibles autour. |
| `OrePreset` | String | `"capsule"` | `"capsule"`, `"cylinder"`, `"ball"`, `"mesh"`. |
| `OreSize` | String | `0.32,0.32,0.75` | Taille (Vector3). |
| `OreMaterial` | String | `"Metal"` | Nom dans `Enum.Material` (sans guillemets dans Studio). |
| `OreColor` | String | `165,170,180` | RGB (0-255). |
| `OreDensity` | Number | 2.0 | Masse volumique. |
| `OreFriction` | Number | 0.20 | Adhérence. |
| `OreElasticity` | Number | 0.00 | Rebond. |
| `OreBoost` | Number | 6 | Force d’éjection. |
| `OreSpin` | Bool | false | Spin visuel. |
| `OreLife` | Number | 12 | Durée avant destruction auto. |
| `OreMeshId` | String | – | MeshId (si preset = `mesh`). |
| `OreTextureId` | String | – | Texture optionnelle. |

---

## 📦 Ce qui est déjà fait

✅ **Base du tycoon** (structure + Items + Buttons).  
✅ `BuildService` (lock/unlock visuel).  
✅ `Purchase.server.lua` (achat via boutons).  
✅ `DropperSystem.server.lua` :

- Spawn dynamique d’ores avec presets.
- Paiement selon `PayoutMode`.
- Physique réaliste (densité, friction, boost).
- Sécurité : max d’ores, destruction auto.

✅ Gestion des **matériaux**, couleurs, tailles via attributs.  
✅ Support des **meshes** (forme libre).  
✅ Support multi-dropper sur un seul convoyeur.  
✅ CollectorHitbox qui crédite seulement les ores `PayOnCollect`.

---

## 📝 Points à venir / Idées

- UI pour afficher Cash, pollution, météo, progression.  
- **Presets** globaux (ex: `PresetName = "Acier"` → charge des valeurs prédéfinies).  
- Système de **claim automatique** (bouton pour prendre un terrain).  
- Animations ou bruitages des droppers.  
- Optimisation pour multi-joueurs (limiter spawn/physique).  
- Sauvegarde des données (cash, progression).

---

## 🚀 Conseils

- Ajuste `MaxOres`, `OreBoost` et la largeur du convoyeur si tu as plusieurs droppers.  
- Laisse un peu d’espace entre les buses de dropper.  
- Utilise `OreValue` pour différencier les gains selon le type de pièce.  
- Si tu veux des formes plus “industrielles”, prépare des MeshParts custom et remplis `OreMeshId`.

> 💡 Avec cette architecture, tu peux créer des dizaines de droppers différents en ne changeant **que les attributs** : plus besoin de modifier le script !
