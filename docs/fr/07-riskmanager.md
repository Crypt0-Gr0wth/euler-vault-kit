# Chapitre 7 — RiskManagerModule : les verifications de compte et de vault, differees par l EVC

`checkAccountStatus` et `checkVaultStatus` sont les deux fonctions que l EVC rappelle systematiquement a la fin de tout batch d operations, jamais directement par un utilisateur : le modificateur `onlyEVCChecks` verifie explicitement `msg.sender == address(evc)` et que l EVC est dans son etat « checks in progress », qui bloque toute reentrance pendant cette phase.

`checkAccountStatus(account, collaterals)` parcourt tous les collateraux actives par le compte et verifie que leur valeur ajustee par la LTV d emprunt (chapitre 8) reste superieure a la valeur de la dette, en utilisant des prix bid/ask asymetriques (chapitre 9) plutot qu un prix unique, une marge de securite supplementaire contre la manipulation de prix a la marge.

`checkVaultStatus` accomplit un role different : ce n est pas une verification de solvabilite individuelle mais une verification globale du vault — mise a jour de l accumulateur d interet, recalcul du taux via le modele de taux (chapitre 12), et verification que les plafonds de depot (`supplyCap`) et d emprunt (`borrowCap`) n ont pas ete depasses par les operations du batch qui vient de s executer, en comparant l etat courant a un instantane (`snapshot`) pris au debut du batch.

[Chapitre suivant : la LTV et sa rampe de reduction progressive](08-ltv.md)
