# Chapitre 2 — GenericFactory : le deploiement permissionless de vaults

`GenericFactory.sol` joue un double role : c est a la fois une fabrique qui deploie de nouveaux vaults et un « beacon » pour ceux qui restent upgradeables. Chaque proxy cree stocke une configuration `ProxyConfig` indiquant s il est upgradeable (auquel cas il pointe toujours vers l implementation courante de la fabrique) ou fige a une implementation precise au moment du deploiement.

Le point notable est la maniere dont les parametres immuables d un vault (l actif sous-jacent, l oracle de prix, l unite de compte) sont transmis : plutot que d etre stockes dans le storage du proxy, ils sont encodes en `trailingData` et ajoutes a la fin de chaque appel delegue au vault — le motif du « meta-proxy » (proche de l EIP-3448, implemente ici par `MetaProxyDeployer`). Le contrat `EVault` les relit depuis le calldata via `ProxyUtils.metadata()` plutot que depuis des variables d etat, ce qui reduit le cout de deploiement de chaque nouveau coffre puisqu aucun `SSTORE` n est necessaire pour ces valeurs fixes.

`initialize(address proxyCreator)` (module `Initialize`, chapitre suivant indirectement) verifie explicitement que la longueur du calldata correspond a la signature plus les metadonnees attendues (`E_ProxyMetadata` sinon), une garde contre un deploiement dont les immuables n auraient pas ete correctement attaches.

[Chapitre suivant : EVault et Dispatch, l architecture modulaire](03-dispatch.md)
