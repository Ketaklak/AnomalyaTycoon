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
