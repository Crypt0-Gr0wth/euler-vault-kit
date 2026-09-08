# Chapitre 11 — GovernanceModule : la configuration du coffre (plafonds, hooks, frais, LTV)

Chaque vault a son propre `governorAdmin`, initialise a l adresse du createur au deploiement (`vaultStorage.creator`, module `Initialize`) mais transferable ou meme renoncable independamment pour chaque instance : la gouvernance de l EVK est deliberement locale a chaque vault plutot que globale au protocole, contrairement au gouverneur unique de MakerDAO ou au multisig central d Aave.

`EVCAuthenticateGovernor` ajoute une garde specifique au-dela de la simple verification du gouverneur : elle interdit explicitement qu un sous-compte (autre que le compte principal) ou qu un operateur autorise via l EVC exerce les pouvoirs de gouvernance, et interdit egalement toute action de gouvernance pendant une operation de « control collateral » en cours — les pouvoirs administratifs ne doivent jamais transiter par les mecanismes de delegation con,us pour les utilisateurs finaux.

Les fonctions de configuration couvrent les plafonds de depot et d emprunt (`setCaps`), les operations desactivables au niveau granulaire via des hooks (`setHookConfig`, chaque operation individuelle du vault peut etre bloquee ou redirigee vers un contrat de hook externe), les frais preleves sur l interet couru (`setInterestFee`), le modele de taux (`setInterestRateModel`, chapitre suivant) et bien sur la LTV de chaque collateral (`setLTV`, chapitre 8).

[Chapitre suivant : le modele de taux d interet, un contrat externe pluggable](12-irm.md)
