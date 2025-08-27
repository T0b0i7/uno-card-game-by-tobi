UNO Card Game (1v1) :flower_playing_cards:

UNO est un jeu de cartes de type “shedding” américain, joué avec un jeu de cartes spécialement imprimé. Les principes généraux du jeu le rapprochent de la famille des “crazy eights” et il est similaire au jeu européen traditionnel mau-mau. Le jeu appartient à la marque Mattel depuis 1992.

🔴 Technologies utilisées : HTML, CSS, JS

<img src="head.png">
Comment ce jeu fonctionne :hourglass:

Le jeu commence automatiquement au chargement.

Le joueur et l’ordinateur (CPU) commencent chacun avec 7 cartes, et une carte numérique démarre la pile de jeu. Le joueur commence. Le joueur peut :

Jouer une carte de la même couleur ou valeur

Jouer une carte Action (Reverse, Skip, Draw 2, Draw 4, Wild)

Si aucune carte jouable n’est disponible, cliquer sur la pile de tirage pour piocher une carte et passer son tour

Ensuite, le CPU joue, en jouant une carte appropriée ou en piochant une carte.

Les cartes Draw 2 (+2) et Draw 4 (+4) ajoutent automatiquement le nombre de cartes à la main de l’adversaire et passent le tour. Reverse et Skip sautent le tour de l’adversaire (avec deux joueurs, Reverse devient un Skip). Les cartes Wild peuvent être jouées à tout moment.

L’objectif immédiat est d’être le premier à ne plus avoir de cartes. Les cartes restantes de l’adversaire sont additionnées selon les règles suivantes :

Cartes numérotées 0-9 = valeur faciale
Reverse, Skip, +2 = 20 pts
Wild, Wild +4 = 50 pts

Le premier joueur à atteindre 100 perd la partie.

Algorithme et flux de jeu :abacus:

Cartes Numériques :

red8 = {
    value: 8,
    point: 8,
    color: 'red',
    changeTurn: true,
    drawValue: 0
}


Cartes Action (valeur croissante pour la logique CPU) :

greenReverse = {
    value: 10,
    point: 20,
    color: 'green',
    changeTurn: false,
    drawValue: 0
}

orangeSkip = {
    value: 11,
    point: 20,
    color: 'yellow',
    changeTurn: false,
    drawValue: 0
}

blueDraw2 = {
    value: 12,
    point: 20,
    color: 'blue',
    changeTurn: true,
    drawValue: 2
}

wild = {
    value: 13,
    point: 50,
    color: 'any',
    changeTurn: true,
    drawValue: 0
}

wild4 = {
    value: 14,
    point: 50,
    color: 'any',
    changeTurn: true,
    drawValue: 4
}


Le gameController utilise changeTurn et drawValue pour déterminer le tour du joueur et si des cartes doivent être piochées.

Comment le CPU joue :computer:

Le CPU garde deux tableaux :

cpuHand = []
playableCards = []


Selon la dernière carte jouée, le CPU parcourt cpuHand et met dans playableCards toutes les cartes jouables, incluant les Wilds.

Pour rendre le CPU stratégique :

Si Math.random() > 0.5 → le CPU priorise les cartes Action pour réduire son score en cas de perte.

Si Math.random() < 0.5 → le CPU garde les cartes Action et joue des cartes Numériques.

Quand le joueur a peu de cartes, le CPU priorise systématiquement les cartes Action.

Comment le joueur ressent le jeu :red_haired_woman::man:

Le gameController suit les cartes jouables du joueur.

Si le joueur clique sur une carte invalide, un message s’affiche.

Ces messages et l’écran de fin de partie sont les seuls prompts pour ne pas distraire le joueur.

Une confirmation “Êtes-vous sûr ?” peut apparaître si le joueur pioche alors qu’il a des cartes jouables.

L’objectif est de créer une boucle de jeu esthétique, minimaliste mais satisfaisante, relaxante et divertissante, pour que les joueurs aient envie de rejouer encore et encore.

Auteur : Eucher ABATTI – Vibe Codeur
