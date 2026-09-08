# Chapitre 4 — VaultModule : le coeur ERC-4626 (deposit, mint, withdraw, redeem)

`VaultModule` implemente l interface ERC-4626 standard (`deposit`, `mint`, `withdraw`, `redeem`, les fonctions `preview*`/`max*`) en s appuyant sur une bibliotheque de types a virgule fixe (`Assets`, `Shares`, definis dans `shared/types/`) plutot que sur des `uint256` bruts, ce qui evite par construction de confondre un montant d actifs avec un nombre de parts a la compilation.

`maxRedeemInternal` illustre une prudence specifique aux credit vaults : si le compte a active un « controller » (un vault ou il a emprunte, chapitre 6), la fonction retourne zero de retrait maximum estime, meme si le solde de parts est non nul. La raison est documentee dans le code : le vault local n a aucun moyen de savoir si le controleur externe autorisera effectivement le retrait lors de la verification de solvabilite en fin de transaction, donc `maxRedeem` sous-estime par prudence plutot que de promettre un montant qui pourrait echouer.

`skim(amount, receiver)` est une fonction additionnelle hors standard ERC-4626 : elle permet de convertir en parts tout exces d actifs transferes directement au contrat (par erreur ou intentionnellement) sans passer par `deposit`, en comparant le solde reel du token au `cash` connu du vault.

[Chapitre suivant : BorrowingModule, emprunter et rembourser](05-borrowing.md)
