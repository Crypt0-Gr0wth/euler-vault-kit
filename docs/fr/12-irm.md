# Chapitre 12 — Le modele de taux d interet : un contrat externe pluggable, IRMLinearKink

A la difference de Compound ou Aave, ou le modele de taux est souvent une bibliotheque interne au contrat de marche, l EVK traite le modele de taux comme un composant totalement externe et interchangeable : chaque vault stocke simplement l adresse d un contrat qui implemente l interface `IIRM`, interrogee via `computeInterestRate(vault, cash, borrows)` a chaque mise a jour de l etat du vault (`checkVaultStatus`, chapitre 7).

`IRMLinearKink.sol` fournit une implementation de reference reconnaissable : le taux croit lineairement avec l utilisation (`borrows / (cash + borrows)`) jusqu a un point de rupture (`kink`), au-dela duquel la pente devient beaucoup plus forte (`slope2`) pour inciter fortement au remboursement ou au depot supplementaire quand la liquidite disponible devient rare — le meme motif de taux « a double pente » deja rencontre dans d autres protocoles de pret, mais ici isole dans un contrat immuable et reutilisable independamment par n importe quel vault.

L interface `computeInterestRate` verifie explicitement `msg.sender == vault`, empechant un contrat tiers d interroger le modele au nom d un vault qu il ne represente pas et d obtenir un effet de bord non voulu (certains IRM plus complexes stockent un etat mutable par vault, ce que garantit cette verification d appelant).

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
