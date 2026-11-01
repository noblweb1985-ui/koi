# Design Adaptatif · Koï

Exercice créatif 01 : deux koïs en WebGL 2 nagent sur une orbite lâche autour du titre et laissent des ondes qui déforment le fond et le texte.

- `index.html` : toute la scène (aucune dépendance, aucun build)
- `assets/` : les deux koïs (WebP transparents) et la police BROKEN

## Comment ça marche

1. **L'eau** : le fond rouge et le titre sont dessinés dans un canvas 2D, puis lus par un shader qui les décale selon la pente des ondes (réfraction).
2. **Les ondes** : 56 anneaux au maximum (x, y, naissance, amplitude) envoyés au shader ; chaque koï en émet un toutes les ~0,15 s derrière son corps, le curseur aussi.
3. **Les koïs** : un maillage de 44 × 9 sommets suit la traînée de la tête. Les coordonnées de texture « déplient » la colonne courbée de l'image ; une onde sinusoïdale fait battre la queue.
4. **La trajectoire** : une ellipse autour du titre dont le rayon et la vitesse varient avec des sinus de fréquences non multiples : le tracé ne se répète jamais exactement.

Mouvement réduit : une image fixe. Sans WebGL 2 : la version HTML (titre + images) reste affichée.
Mode test : `?test` puis `__koi(secondes)` dans la console fait avancer la simulation à pas fixe.
