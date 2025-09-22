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


# ✅ Eco-Tycoon — TODO

> Liste de tâches priorisées pour passer d’un prototype jouable à un tycoon multi propre. Coche ce que tu termines 😉

---

## 🔴 PRIORITÉ 0 — Bloquants (à faire maintenant)
- [ ] **Séparer décor & achetables** dans `Items/` (ou marquer `Purchasable=true` uniquement sur les items achetables).
- [ ] Vérifier que **ConveyorDecor** (conveyor + crate + `CollectorHitbox`) est **hors** du modèle achetable.
- [ ] Sur chaque bouton d’achat : `ItemId` (nom exact de l’item) + `Cost` (number) + `ProximityPrompt` actif.
- [ ] Sur chaque *dropper* : attribuer `OwnerUserId` **à l’achat** (déjà géré par `onUnlocked` → tag `Machine`).
- [ ] Dans `DropperSystem`: s’assurer que **PayoutMode** est **cohérent** :
  - `loop` ⇒ paiement au tick **uniquement**
  - `collect` ⇒ paiement **uniquement** à la `CollectorHitbox`
- [ ] Tester un run complet (acheter → spawn → convoyeur → collecte → cash correct et stable).

---

## 🟠 PRIORITÉ 1 — UI minimale (jouable)
- [ ] **UI Cash** (ScreenGui + TextLabel en haut) qui lit `leaderstats.Cash` (LocalScript).
- [ ] **Feedback achat**: popup “+X$” ou tween sur le cash lors d’un achat.
- [ ] **Prompt distance**: ajuster `ProximityPrompt.MaxActivationDistance` (=10–14) et `HoldDuration` (=0.2).

---

## 🟠 PRIORITÉ 2 — Droppers multiples & presets
- [ ] Dupliquer `TycoonDropper` → `TycoonDropper_Acier`, `_Cuivre`, `_Plastique` (exemple).
- [ ] Attributs par dropper :
  - [ ] `OrePreset` / `OreSize` / `OreColor` / `OreMaterial`
  - [ ] `OreValue` / `BaseInterval` / `PayoutMode`
  - [ ] `MaxOres` / `OreBoost` / `OreDensity` / `OreFriction`
- [ ] **Espacement** des buses sur le convoyeur (4–5 studs min).
- [ ] Élargir / guider la **caisse** (bords + petit toit invisible si besoin).

---

## 🟡 PRIORITÉ 3 — Écosystème & équilibrage
- [ ] Brancher les tags `Emitter` / `Mitigator` + `EmissionRate` / `MitigationRate` sur certains items.
- [ ] Vérifier `Env.GetZoneEfficiency(zoneId)` et son impact réel sur le tick (valeurs 0.5–1.5).
- [ ] **Équilibrer**: `OreValue × fréquence` ≈ progression fun (premier item acheté < 30 sec).

---

## 🟢 PRIORITÉ 4 — Qualité de vie
- [ ] **Hologramme**: vérifier `BuildService` (ForceField + `HOLO_ALPHA`) et que `CollectorHitbox` reste invisible.
- [ ] **AlwaysVisible/NoBuildFade**: tags optionnels pour ignorer certains Parts si décor inclus.
- [ ] **Diagnostics**: conserver les prints `"[Purchase]"` & `"[Dropper]"` pendant le dev, désactiver en prod.
- [ ] **Couleurs/conventions**: palette métal (acier, cuivre, alu) + cohérence UI (typo, marges).

---

## 🔵 PRIORITÉ 5 — Multi & sécurité
- [ ] **ClaimPad**: un pad par `Tycoon_X` avec `ProximityPrompt` pour set `OwnerUserId` et activer les boutons.
- [ ] **Vérification serveur**: avant achat, s’assurer que `player.UserId == tycoon.OwnerUserId`.
- [ ] **Isolation**: éviter que les ores d’un tycoon entrent dans la caisse d’un autre (distance/hauteur/pare-chocs).
- [ ] **Perf**: limiter `MaxOres`, `OreLife` (=8–12), et éviter  >8 droppers actifs / tycoon au début.

---

## 🟣 PRIORITÉ 6 — Contenu futur (nice to have)
- [ ] **UI pollution/météo** avec barres et tooltips.
- [ ] **Améliorations** de droppers (tiers) : vitesse, valeur, rendement.
- [ ] **Prestige** / reset soft.
- [ ] **SFX**: *plop* discret à la sortie, *clang* feutré à la caisse (volume très bas).
- [ ] **DataStore**: sauvegarde `Cash`, items achetés, améliorations.

---

## 🔧 Checklists rapides

### Attributs dropper type “loop”
- [ ] `Purchasable=true`
- [ ] `PayoutMode="loop"`
- [ ] `OreValue=1..5`
- [ ] `BaseInterval=1.5..3`
- [ ] `OrePreset="capsule"`
- [ ] `OreSize="0.32,0.32,0.75"`
- [ ] `OreMaterial=Metal`
- [ ] `OreColor="165,170,180"`
- [ ] `MaxOres=10`
- [ ] `OreBoost=6`
- [ ] `OreDensity=2.0`, `OreFriction=0.2`, `OreElasticity=0.0`

### Attributs dropper type “collect”
- [ ] `Purchasable=true`
- [ ] `PayoutMode="collect"`
- [ ] `OreValue=3..10`
- [ ] `BaseInterval=2..4`
- [ ] `CollectorHitbox` bien placée dans la caisse
- [ ] `OreLife=12`
- [ ] `MaxOres=12`

---

## 🧪 Scénarios de test (rapides)
- [ ] Achat d’un dropper → hologramme → apparition rapide → spawn ore.
- [ ] `PayoutMode="loop"`: cash +X **à chaque tick** (stable).
- [ ] `PayoutMode="collect"`: cash **0 au tick**, +Value **à la caisse**.
- [ ] Plusieurs droppers sur un même convoyeur sans embouteillage.
- [ ] Rejoin : scripts fonctionnent, pas de double-boucles (`_LoopStarted` respected).
- [ ] Pas d’accumulation d’ores (collector détruit bien, Debris ok).

---

## 🗺️ Organisation hiérarchie (rappel)
```
Tycoon_1
 ├─ Items
 │   ├─ TycoonDropper_Acier   (Purchasable=true, Machine, etc.)
 │   ├─ TycoonDropper_Cuivre  (Purchasable=true, Machine, etc.)
 │   └─ ConveyorDecor         (décor permanent + CollectorHitbox)
 └─ Buttons
     ├─ Btn_TycoonDropper_Acier (Part+Prompt → ItemId="TycoonDropper_Acier", Cost=...)
     └─ Btn_TycoonDropper_Cuivre
```
