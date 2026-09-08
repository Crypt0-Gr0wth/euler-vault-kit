# Chapitre 9 — LiquidityUtils : prix bid/ask pour les comptes sains, prix median pour la liquidation

`calculateLiquidity` et `checkLiquidity` (utilisees respectivement pour les vues externes et pour la verification de statut obligatoire) partagent la meme logique de fond mais illustrent un choix de conception delibere sur les prix utilises : lors d une verification normale de solvabilite (`checkLiquidity`), le code interroge l oracle avec `getQuotes`, qui retourne separement un prix bid et un prix ask, et retient systematiquement le prix le moins favorable au compte (ask pour la dette, bid pour le collateral).

Lors d une liquidation potentielle en revanche (`liquidation == true`), le code bascule sur `getQuote`, un prix median unique. Le commentaire du code est explicite : utiliser un ecart bid/ask dans le contexte de la verification de compte cree une marge de securite qui empeche un compte legerement sous-collateralise en apparence d etre en realite sain, mais cette meme marge ne doit pas etre appliquee lors du calcul du montant exact liquidable, ou elle fausserait le calcul de la decote de liquidation.

`getCollateralValue` applique la LTV du collateral concerne (`getLTV`) directement au montant en unite de compte, avant meme de comparer a la dette : un collateral dont la LTV a ete mise a zero par la gouvernance ne compte plus du tout, meme si son solde reste positif sur le compte.

[Chapitre suivant : LiquidationModule, le liquidateur reprend la dette](10-liquidation.md)
