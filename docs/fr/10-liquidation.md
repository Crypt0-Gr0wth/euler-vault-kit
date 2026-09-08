# Chapitre 10 — LiquidationModule : le liquidateur reprend la dette, decote bornee, et socialisation

`liquidate(violator, collateral, repayAssets, minYieldBalance)` fonctionne differemment des liquidations a repaiement direct d Aave ou Compound : plutot que d envoyer des actifs pour rembourser la dette du compte viole, le liquidateur reprend litteralement la dette a son propre compte via `transferBorrow` (le meme mecanisme que `pullDebt` du chapitre 5), puis recoit en echange une part du collateral du compte viole via `enforceCollateralTransfer`, avec une decote calculee par `calculateMaxLiquidation`.

Plusieurs gardes protegent contre les abus : l auto-liquidation est interdite (`E_SelfLiquidation`), seuls les collateraux explicitement reconnus par le vault peuvent etre saisis, et surtout une periode de repit (`liquidationCoolOffTime`) doit s ecouler depuis la derniere verification de statut reussie du compte avant qu il puisse etre liquide — une protection specifique contre les attaques d auto-liquidation ou un attaquant manipulerait artificiellement son propre etat pour en profiter immediatement.

Le facteur de decote est plafonne par `maxLiquidationDiscount` (parametre de gouvernance) : meme si le score de sante du compte est tres degrade, le liquidateur ne peut jamais recevoir plus qu un multiple fixe de la valeur qu il reprend en dette. Si, apres la liquidation, le compte viole n a plus aucun collateral mais garde une dette residuelle, celle-ci est socialisee : `decreaseBorrow` l efface directement, la perte etant silencieusement absorbee par l ensemble des deposants du vault via la baisse du taux de change parts/actifs.

[Chapitre suivant : GovernanceModule, la configuration du coffre](11-governance.md)
