# Exercice Technique pour developpeur front-end @Destygo

## Objectif

Le but de l’exercice est de réaliser l’interface pour mettre en place des Quick Reply comme suit:



On donne les précisions suivantes:
1. Text content, templates et Quick Replies sont toutes les 3 des box collapsible. Il faut remplir les contenus de Text Content et Templates avec un texte aléatoire.
2. Les Quick Reply sont Reorderable, on remarquera l’image à gauche d’une QR qui apparaît au hover et qui permet de réordonner les QR par la valeur order_index de l’objet.

## Utilisation du repo



## Data de départ

On donne la structure de départ en json pour les QR suivante (elle est egalement initialise dans le fichier de depart):
```
[
    {
        "button_type": "postback",
        "order_index": 1,
        "title": "☝️ First button",
        "payload": "I will send first",
        "is_loop": false
    },
    {
        "button_type": "postback",
        "order_index": 1,
        "title": "✌️ second button",
        "payload": "I will send two",
        "is_loop": true
    },
    {
        "button_type": "postback",
        "order_index": 2,
        "title": "Third button",
        "payload": "I will send 3",
        "is_loop": false
    }
]
```

## Librairies utiles

Le candidat peut utiliser les librairies suivvante s’il en voit l’utilite:
- vue.Dragabble https://github.com/SortableJS/Vue.Draggable
- vue-slide-up-down https://github.com/danieldiekmeier/vue-slide-up-down
- vue-animate https://github.com/asika32764/vue2-animate
