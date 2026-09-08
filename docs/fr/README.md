# Parcours francais de l Euler Vault Kit — Pret et emprunt

Lecture commentee du kit de construction de coffres de credit Euler (EVK), en francais, un mecanisme par chapitre.
Aucun code n a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de l Euler Vault Kit](01-presentation.md)
2. [GenericFactory : le deploiement permissionless de vaults](02-factory.md)
3. [EVault et Dispatch : l architecture modulaire par delegatecall](03-dispatch.md)
4. [VaultModule : le coeur ERC-4626 (deposit, mint, withdraw, redeem)](04-vault.md)
5. [BorrowingModule : emprunter, rembourser et le flash loan](05-borrowing.md)
6. [L Ethereum Vault Connector (EVC) : un systeme de collateralisation partage entre vaults](06-evc.md)
7. [RiskManagerModule : les verifications de compte et de vault, differees par l EVC](07-riskmanager.md)
8. [La LTV et sa rampe de reduction progressive, volontairement asymetrique](08-ltv.md)
9. [LiquidityUtils : prix bid/ask pour les comptes sains, prix median pour la liquidation](09-liquidityutils.md)
10. [LiquidationModule : le liquidateur reprend la dette, decote bornee, et socialisation](10-liquidation.md)
11. [GovernanceModule : la configuration du coffre (plafonds, hooks, frais, LTV)](11-governance.md)
12. [Le modele de taux d interet : un contrat externe pluggable, IRMLinearKink](12-irm.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
