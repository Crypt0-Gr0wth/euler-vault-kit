# Chapitre 8 — La LTV et sa rampe de reduction progressive, volontairement asymetrique

Chaque vault maintient une LTV (loan-to-value) distincte pour chaque collateral qu il accepte, stockee dans `ltvLookup` et geree par `LTVUtils.sol`. Deux valeurs coexistent : une LTV d emprunt (`borrowLTV`, utilisee lors des verifications normales de solvabilite) et une LTV de liquidation (`liquidationLTV`, generalement plus permissive, utilisee uniquement lors des liquidations).

Le trait le plus distinctif est la gestion du temps dans `setLTV` (module `Governance`) : si la gouvernance augmente une LTV, le changement est immediat. Mais si elle la reduit, le nouveau seuil de liquidation n entre en vigueur que progressivement, via une rampe lineaire entre l ancienne valeur et la cible sur une duree `rampDuration` choisie par la gouvernance. Le calcul (`LTVConfig.getLTV`) interpole lineairement en fonction du temps restant jusqu a `targetTimestamp`.

Cette asymetrie deliberee protege les emprunteurs existants : un durcissement soudain des conditions ne peut pas precipiter instantanement des comptes sains vers la liquidation, alors qu un assouplissement (plus de marge pour les emprunteurs) ne presente aucun risque a etre applique immediatement. Le code interdit meme explicitement de combiner une augmentation de la LTV de liquidation avec une rampe (`E_LTVLiquidation`), la rampe n ayant de sens que pour une reduction.

[Chapitre suivant : LiquidityUtils, prix bid/ask contre prix median](09-liquidityutils.md)
