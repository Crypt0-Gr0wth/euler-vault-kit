# Chapitre 3 — EVault et Dispatch : l architecture modulaire par delegatecall

Le contrat `EVault` deploye par la fabrique n implemente presque aucune logique lui-meme : il herite de `Dispatch`, qui a son tour herite de sept modules abstraits (`Initialize`, `Token`, `Vault`, `Borrowing`, `Liquidation`, `RiskManager`, `BalanceForwarder`, `Governance`). Chaque module est aussi deploye separement comme un contrat independant, et son adresse est enregistree comme immuable dans `Dispatch` au moment de la construction (`DeployedModules`).

Ce n est pas un « diamond » standard (EIP-2535) a table de routage modifiable en storage : les adresses de modules sont figees a la compilation pour chaque implementation d `EVault`, ce qui est deliberement plus rigide mais evite le cout et les risques d une table de selecteurs mutable. Le routage se fait via le modificateur `use(module)`, qui laisse le corps de la fonction publique vide puis delegue l appel complet au module concerne en assembleur bas niveau (`delegateToModule`).

Un detail d ingenierie notable : les fonctions `view` ne peuvent pas utiliser `delegatecall` directement en Solidity. Le contrat contourne cette limite avec `useView(module)`, qui fait un `staticcall` sur `this.viewDelegate()` — une fonction externe qui, elle, peut faire le `delegatecall` reel vers le module, le tout enveloppe dans un appel statique qui preserve la garantie de non-mutation.

[Chapitre suivant : VaultModule, le coeur ERC-4626](04-vault.md)
