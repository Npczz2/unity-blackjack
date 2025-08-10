# Unity Blackjack
This is a minigame created with **Unity** using **C#** for a game jam project.
The main idea of this repository is to show **the game flow and the AI's thinking process**.

![Blackjack1](https://github.com/Npczz2/unity-blackjack/blob/main/Blackjack%20Images/blackjack1Gif.gif)

# How does blackjack work?
In classic blackjack, the player needs to buy cards to get a hand value **as close to 21 as possible** while he tries to beat the dealer's hand. If you exceed this value, you lose.

The player has two possible actions while playing: **Hit or stay.** Hitting gives him another card and stay means he stops buying.

If the player's hand value is higher than the dealer's, he wins and vice versa.

# Blackjack implemented in Unity
## Game manager
In the main script, there is an array that stores all the deck cards. These cards are **Scriptable objects** that contain the card **value** and **sprite**.

![Scriptable](https://github.com/Npczz2/unity-blackjack/blob/main/Blackjack%20Images/scriptableObject.png)

The game manager controls the turns, alternating between the player and the dealer, stores their scores and if they stopped buying.

## Enemy's logic
The enemy thinking process is based on the player score. If the player score is higher than 21, the enemy stops buying and wins the round. If not, the logic starts.
```
if(enemyValue <= 11) { 
    enemyBuy(); //1
} else {
    if(playerStop) { //2
        if(playerValue > enemyValue) {
            enemyBuy(); //2.1
        } else {
            enemyStop = true; //2.2
        }
    } else { //3
        if(enemyValue <= 15) {
            enemyBuy(); //3.1
        } else {
            if(playerValue <= 21 && playerValue > enemyValue) {
                enemyBuy(); //3.2
            } else {
                enemyStop = true; //3.3
            }
        }
    }
}
```
*1: The maximum value you can get buying a card is 10, meaning that the enemy will always buy if the value is lower or equal to 11*

*2: There are two possible paths when the player has stopped buying.*

- *2.1: If the player value is higher than the enemy's, he will buy even if it's risky, because if he stops he will lose anyways.*
    
- *2.2: If the enemy's score meets the player's one value or pass it, he will stop buying (in this scenario the enemy consider a draw).*
    
*3: If the player hasn't stopped buying, the enemy needs to keep playing.*

- *3.1: The enemy can't stop if his score is lower than 15 because the value is too low and can be beaten easily.*
    
- *3.2: If the enemy's score is greater than 15 and the player value is still higher than his, he needs to buy even if it's risky.*
    
- *3.3: However, if the player's score isn't higher than his, he stops buying.*

## Player's logic
Just like the enemy, the player has the option to hit or stop whenever he wants.

![HitOrStand](https://github.com/Npczz2/unity-blackjack/blob/main/Blackjack%20Images/hitOrStand.png)

## Calculating the winner
The program will then check the scores and finding out who the winner is.
```
void checkResults() {
    if(enemyValue > 21 && playerValue > 21) { //1
        restartGame();
    } else if(enemyValue > 21 || playerValue > 21) { //2
        if(enemyValue > 21) {
            playerWin();
        } else if(playerValue > 21) {
            enemyWin();
        }
    } else { //3
        if(enemyValue > playerValue) {
            enemyWin();
        } else if(enemyValue < playerValue) {
            playerWin();
        } else {
            restartGame();
        }
    }
}
```
*1: If both players exceeded 21 on their scores, the game will consider it a draw.*

*2: If one of them exceeded the value, the other one will get a point.*

*3: If none of them exceeded it, the one with the higher score wins. If the score is the same, it will be considered a draw.*

# The game
This minigame is a part of the game Sirin, that is available at: https://npcproductions.itch.io/sirin

![Blackjack2](https://github.com/Npczz2/unity-blackjack/blob/main/Blackjack%20Images/blackjack2Gif.gif)
