# Technical test for Front-end developer @Destygo

## Objective

The objective of the test is to build the following interface to set-up Quick Replies (shortcuts in chatbot interfaces):

![objective_qr](https://s3.eu-central-1.amazonaws.com/destygo-public/assets/img/images/QuickRepliesObjective.jpg)

We give the following details:
1. `Text content`, `templates` and `Quick replies` are all collapsible box. For `Text content` and `templates`, the box content has to be random text.
2. Quick-replies are orderable, you can change their `order_index` fields that are linked to the order they will appear.

## Use the repository

To facilitate the work of the candidate, the repository was built with VueCLI. To use it, just start in your terminal the following commands:
```
$> yarn install
$> yarn serve
```

Please be sure to work on a fork or branch of this repository to make easy the evaluation of your code.

## Start data

We give the following starting state (in JSON, you will find it in the code too):
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

The data above will of course change as quick replies are added or removed respectively.

## Useful libs

The candidate can use any javascript librairies he finds relevant. If he does not have any idea, he can use one of the followings:
- vue.Dragabble https://github.com/SortableJS/Vue.Draggable
- vue-slide-up-down https://github.com/danieldiekmeier/vue-slide-up-down
- vue-animate https://github.com/asika32764/vue2-animate
