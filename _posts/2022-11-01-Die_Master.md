---
title:  "Die Master"
layout: post
categories: media
---

![Die Master App Icon](/assets/DM_Icon.png)


Application I wrote and published to the [App Store](https://apps.apple.com/us/app/die-master/id6443835851), which helps DM's track encounters in role-playing games. My goals with this application was twofold. One create a robust rolling system that tracked past roles and accounted for the variety of different events types that can occur while playing a role-playing game. Second, handle JSON in such a way that the app can ingest new monsters and characters easily.

The crux of making my roll system robust is my Event struct. This records any action that the user can take rolling a dice, making an attack, activating an ability, etc. What values are optional suddenly changes the way the application chooses to display the event.

![Image of Goblin - Scimitar](/assets/DMImage1.png)

![Image of Goblin - nimble escape](/assets/DmImage2.png)

![Image of Goblin - damage](/assets/DMImage3.png)

All of the above views have the same exact Event struct providing the data, but SwiftUI treats them completely differently, providing unique displays depending on what the important information is. It's a small thing, but I feel it shows a significant improvement from my first application, in terms of understanding and utilizing the power of SwiftUI combined with MVVM.

As for the backend, the application can except JSON (like what is shown below) and converted into monsters that the app maintains in storage. This would make it much easier for users to eventually be able to share content that they have created.

```JSON
[
  {
    "abilaty": [
      {
        "id": "9ED8654D-3886-498C-B9F0-B30A92AB5247",
        "name": "Brute",
        "discription": " A melee weapon deals one extra die of its damage when the bugbear hits with it (included in the attack)."
      },
      {
        "discription": "If the bugbear surprises a creature and hits it with an attack during the first round of combat, the target takes an extra 7 (2d6) damage from the attack.",
        "id": "CCA91B9A-3061-4544-8654-22231C2163E9",
        "name": "Surprise Attack",
        "onHit": {
          "numberOfDice": 2,
          "numberOfSides": 6,
          "toAdd": 0
        }
      },
      {
        "id": "A776E7A0-90D2-4DAE-8A0B-99B585CB002F",
        "name": "Morningstar",
        "roll": {
          "numberOfDice": 1,
          "numberOfSides": 20,
          "toAdd": 2
        },
        "onHit": {
          "numberOfDice": 2,
          "numberOfSides": 8,
          "toAdd": 2
        }
      },
      {
        "discription": "range 30/120 ft.",
        "id": "7C459A49-9710-4CB7-9BDA-DD5071C25537",
        "name": "Javelin",
        "roll": {
          "numberOfDice": 1,
          "numberOfSides": 20,
          "toAdd": 4
        },
        "onHit": {
          "numberOfDice": 1,
          "numberOfSides": 6,
          "toAdd": 2
        }
      }
    ],
    "id": "966E5EB7-BA6B-4390-B48D-9E26BD1988E6",
    "isShowing": true,
    "OGLContent": true,
    "name": "Bugbear"
  }
]
```
