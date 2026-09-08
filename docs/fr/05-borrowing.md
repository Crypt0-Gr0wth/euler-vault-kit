# Chapitre 5 — BorrowingModule : emprunter, rembourser et le flash loan

`borrow(amount, receiver)` transfere des actifs disponibles (`cash`) a l emprunteur et augmente sa dette, mais ne verifie pas immediatement la solvabilite du compte : cette verification est differee et executee par l EVC en fin de transaction (chapitre 6 et 7), ce qui permet d enchainer plusieurs operations (par exemple deposer un collateral puis emprunter dans la meme transaction) sans etre bloque par un etat intermediaire temporairement insolvable.

`repayWithShares` est une fonction distinctive : elle permet de rembourser une dette directement avec les parts (EToken) detenues dans le vault sous-jacent, en brulant a la fois les parts de depot et la dette en une seule operation — utile pour fermer une position sans avoir a retirer puis redeposer les actifs.

`pullDebt(amount, from)` permet a un compte de reprendre a son compte la dette d un autre compte (avec le consentement implicite via l EVC, puisque l appel doit venir d une operation autorisee) : c est exactement ce mecanisme qui est reutilise par le module de liquidation (chapitre 10) pour transferer la dette du compte liquide vers le liquidateur.

`flashLoan(amount, data)` suit le motif desormais standard : transfert immediat des actifs, callback `onFlashLoan` sur l appelant, puis verification que le solde du contrat a ete restaure avant la fin de la transaction — sans frais explicite code en dur dans cette fonction, contrairement a certains flash loans a frais fixes.

[Chapitre suivant : l Ethereum Vault Connector, le systeme de collateralisation partage](06-evc.md)
