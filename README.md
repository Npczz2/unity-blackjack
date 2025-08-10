# Unity Blackjack
This is a minigame created with Unity using C# for a game jam project.
The main idea of this repository is to show the game flow and the AI's thinking process.

//Gif de gameplay

# How blackjack works?
In classic blackjack, the player needs to buy cards to get a hand value as close to 21 as possible while he tries to beat the dealer's hand. If you exceed this value, you lose.
The player has two possible actions while playing: Hit or stay. Hitting gives him another card and stay means he stopped buying.
If the player's hand value is higher than the dealer's one, he wins and vice versa.

# Blackjack implemented in Unity
## Game manager
In the main script, there is an array that stores all the deck cards. These cards are **Scriptable objects** that contains the card **value** and **sprite**.

//Imagem do scriptable object do lado da sprite

The game manager controls the turns, alternating between the player and the dealer, stores their scores and if they stopped buying.

## Enemy logic
The enemy thinking process is based on the player score. If the player score is higher than 21, the enemy stops buying and win the round. If not, the logic starts.
```
if(enemyValue <= 11) {
    enemyBuy();
} else {
    if(playerStop) {
        if(playerValue > enemyValue) {
            enemyBuy();
        } else {
            enemyStop = true;
        }
    } else {
        if(enemyValue <= 15) {
            enemyBuy();
        } else {
            if(playerValue <= 21 && playerValue > enemyValue) {
                enemyBuy();
            } else {
                enemyStop = true;
            }
        }
    }
}
```
