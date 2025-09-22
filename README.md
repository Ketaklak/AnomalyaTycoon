# ✅ Eco-Tycoon — TODO (MAJ 2025-09-22)

> Objectif : passer d’un proto jouable à un tycoon multi propre. Coche et enchaîne.

---

## 🔴 PRIORITÉ 0 — Bloquants
- [ ] Sur chaque bouton d’achat : `ItemId` (nom exact) + `Cost` (number) + `ProximityPrompt` actif.
- [x] Sur chaque *dropper* : attribuer `OwnerUserId` **à l’achat** — fait dans `Purchase.onUnlocked`.
- [x] `DropperSystem` — **PayoutMode** cohérent :
  - `loop` ⇒ paiement **au tick uniquement**
  - `collect` ⇒ paiement **uniquement** à la caisse (`CollectorHitbox`)
- [x] Anti double-paiement à la caisse : flag `PayOnCollect` sur l’ore **+** registre global `CollectedOnce`.
- [x] Run complet validé (acheter → spawn → convoyeur → collecte → cash stable).

**Rappels**
- `OreMaterial` = texte (ex. `Metal`) → conversion via `Enum.Material[name]`.
- `spawnPhysicalOre(dropperModel, payoutMode)` passe le mode pour marquer `PayOnCollect`.

---

## 🟠 PRIORITÉ 1 — UI minimale (jouable)
- [x] **UI Cash** (HUD) lisant `leaderstats.Cash` (LocalScript).
- [x] **Feedback achat** : popup **±X$** + **pulse** du HUD.
- [x] **ProximityPrompt** : `MaxActivationDistance=12`, `HoldDuration=0.2`, `RequiresLineOfSight=false`.

---

## 🟠 PRIORITÉ 2 — Droppers multiples & presets (NEXT)
- [ ] Dupliquer `TycoonDropper` → `TycoonDropper_Acier`, `_Cuivre`, `_Plastique` (exemples).
- [ ] Attributs par dropper :
  - [ ] `OrePreset` / `OreSize` / `OreColor` / `OreMaterial`
  - [ ] `OreValue` / `BaseInterval` / `PayoutMode`
  - [ ] `MaxOres` / `OreBoost` / `OreDensity` / `OreFriction` / `OreElasticity` / `OreLife`
- [ ] **Espacement** des buses sur le convoyeur (≥ 4–5 studs).
- [ ] Élargir / guider la **caisse** (rebords + éventuel toit invisible).

---

## 🟡 PRIORITÉ 3 — Écosystème & équilibrage
- [ ] Brancher tags `Emitter` / `Mitigator` (+ `EmissionRate` / `MitigationRate`) sur certains items.
- [ ] Vérifier `Env.GetZoneEfficiency(zoneId)` et son impact réel (0.5–1.5).
- [ ] **Équilibrage**: `OreValue × fréquence` pour progression fun (premier achat < 30s).
- [ ] Varier droppers (poids/valeur/cadence) pour un workflow industriel.

---

## 🟢 PRIORITÉ 4 — Qualité de vie
- [ ] **Hologramme**: `BuildService` (ForceField + `HOLO_ALPHA`), `CollectorHitbox` invisible.
- [ ] Tags **AlwaysVisible/NoBuildFade** pour ignorer des parts décor.
- [ ] **Diagnostics**: garder logs `"[Purchase]"`, `"[Dropper]"` en dev; mute en prod.
- [ ] **Cohérence** UI & couleurs (palette métal, typo, marges).

---

## 🔵 PRIORITÉ 5 — Multi & sécurité
- [ ] **ClaimPad** par `Tycoon_X` (Prompt) pour set `OwnerUserId` et activer les boutons.
- [ ] **Vérification serveur** avant achat : `player.UserId == tycoon.OwnerUserId`.
- [ ] **Isolation** : éviter que des ores d’un tycoon scorent dans une autre caisse.
- [ ] **Perf** : limiter `MaxOres`, `OreLife` (=8–12), < 8 droppers actifs/tycoon au début.

---

## 🟣 PRIORITÉ 6 — Contenu futur
- [ ] **UI pollution/météo** (barres + tooltips).
- [ ] **Améliorations** de droppers (tiers).
- [ ] **Prestige** / soft reset.
- [ ] **SFX** discrets (sortie & caisse).
- [ ] **DataStore**: sauvegarde `Cash`, items, upgrades.

---

## 🔧 Checklists rapides

### Dropper type “loop”
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

### Dropper type “collect”
- [ ] `Purchasable=true`
- [ ] `PayoutMode="collect"`
- [ ] `OreValue=3..10`
- [ ] `BaseInterval=2..4`
- [ ] `CollectorHitbox` bien placée
- [ ] `OreLife=12`
- [ ] `MaxOres=12`
- [ ] Vérif : marque bien les ores `PayOnCollect=true` (auto via spawner).

---

## 🧪 Scénarios de test
- [ ] Achat d’un dropper → hologramme → spawn ore rapide.
- [ ] `loop` : +cash **à chaque tick** (stable).
- [ ] `collect` : +cash **uniquement** à la caisse (une seule fois/ore).
- [ ] Plusieurs droppers sans embouteillage.
- [ ] Rejoin : pas de double-boucles (`_LoopStarted` respecté).
- [ ] Collector détruit bien les ores (pas d’accumulation, Debris ok).

---

## 🗺️ Hiérarchie (rappel)
Tycoon_1
├─ Items
│  ├─ TycoonDropper_Acier (Purchasable=true, …)
│  ├─ TycoonDropper_Cuivre (Purchasable=true, …)
│  └─ ConveyorDecor (décor permanent + CollectorHitbox)
└─ Buttons
   ├─ Btn_TycoonDropper_Acier (ItemId="TycoonDropper_Acier", Cost=…)
   └─ Btn_TycoonDropper_Cuivre
