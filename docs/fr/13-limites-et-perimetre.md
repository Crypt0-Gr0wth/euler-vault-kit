# Chapitre 13 — Limites connues et perimetre de ce parcours

Le code de l Euler Vault Kit est publie sous deux licences distinctes selon les fichiers : GPL-2.0-or-later pour la majorite du depot, mais Business Source License 1.1 pour les fichiers de `src/EVault/modules/` specifiquement, avec une date de conversion automatique vers GPL-2.0-or-later fixee au 24 avril 2029 (indiquee dans le README et le fichier LICENSE).

Ce parcours ne couvre pas en detail `src/Synths/` (jetons synthetiques), `src/ProtocolConfig/` (parametres globaux de frais au niveau protocole), `src/SequenceRegistry/` (attribution des symboles de coffres), le detail complet de `BalanceUtils.sol` et `Cache.sol` (gestion bas niveau du cache de vault et des soldes), ni le contrat externe `EthereumVaultConnector` lui-meme, importe comme dependance et non present dans ce depot — seule son interface cote client (`EVCClient.sol`) a ete detaillee.

Rien n a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit sa propre suite de tests Foundry (dossier `test/`) et des tests d invariants (Echidna, Medusa) pour verification independante.
