# Chapitre 6 — L Ethereum Vault Connector (EVC) : un systeme de collateralisation partage entre vaults

L EVC est un contrat externe au depot EVK (importe comme dependance) qui joue le role de chef d orchestre entre tous les vaults independants deployes par la fabrique. Il gere les « sous-comptes virtuels » (jusqu a 256 par adresse principale, derives par XOR sur les derniers bits de l adresse), la liste des collateraux actives par un compte, et surtout le controleur : le vault unique aupres duquel un compte peut avoir une dette active a un instant donne.

`EVCClient.sol` fournit les utilitaires qui permettent a chaque module d `EVault` de dialoguer avec l EVC : `EVCAuthenticate` recupere l identite reelle de l appelant (le compte « pour le compte de qui » l EVC execute l appel, qui peut differer de `msg.sender` lors d operations groupees), tandis que `EVCAuthenticateDeferred` verifie en plus que l appel passe bien par l EVC et que les verifications de statut sont actuellement differees.

Le modificateur `callThroughEVC` (dans `Dispatch.sol`, chapitre 3) garantit qu aucune fonction sensible du vault ne peut etre executee en dehors du cadre de l EVC : un appel direct au vault est automatiquement redirige vers `EVC.call`, qui rappelle ensuite le vault avec le meme calldata mais cette fois dans le contexte correct ou les verifications de compte et de vault seront differees jusqu a la fin du batch plutot qu executees immediatement.

[Chapitre suivant : RiskManagerModule, les verifications differees](07-riskmanager.md)
