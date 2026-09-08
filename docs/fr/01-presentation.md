# Chapitre 1 — Presentation de l Euler Vault Kit

L Euler Vault Kit (EVK) n est pas un protocole de pret unique mais un kit pour construire des « credit vaults » : des coffres ERC-4626 augmentes d une fonction d emprunt. A la difference d un coffre ERC-4626 classique qui investit activement les fonds deposes pour generer du rendement, un credit vault est un pool de pret passif — le rendement provient exclusivement des interets payes par les emprunteurs.

N importe qui peut deployer son propre credit vault via une fabrique permissionless (chapitre 2), en choisissant son actif, son oracle de prix et son unite de compte. Chaque vault peut ensuite servir de collateral pour n importe quel autre vault du systeme grace a l Ethereum Vault Connector (EVC, chapitre 6), un contrat externe qui orchestre les comptes virtuels, les controleurs d emprunt et les verifications de solvabilite differees. C est ce decouplage entre vaults independants et systeme de collateralisation partage qui distingue l EVK des pools geres de facon monolithique comme Aave ou Compound.

Ce parcours s appuie sur le depot clone a la date d ecriture. Fichiers centraux : `src/EVault/EVault.sol`, `src/EVault/Dispatch.sol`, `src/EVault/modules/` (Vault, Borrowing, Liquidation, RiskManager, Governance, Initialize, BalanceForwarder), `src/EVault/shared/` (LiquidityUtils, LTVUtils, EVCClient), `src/GenericFactory/GenericFactory.sol` et `src/InterestRateModels/IRMLinearKink.sol`.

Rien n a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : GenericFactory, le deploiement permissionless](02-factory.md)
