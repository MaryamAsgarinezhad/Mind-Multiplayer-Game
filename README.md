# Mind-Multiplayer-Game

Description of the game
The mind game is a collaborative game. In it, players try to beat the numbers by cooperating with each other. In this way, without seeing each other's cards, players must determine whether the lowest card is in their hand or not.

- cards
Numbers: The cards have numbers from 1 to 100, which are dealt at the beginning of each round and placed in the hands of the players in each stage according to the stage number.

Stage card: indicates the current stage of the game.

Heart card: As many players as the number of players, we must have heart cards in the game. These cards are shared by all players.

Ninja card: Players can use this card as they wish, and after that each player must play the lowest number they have. At the beginning of the game, we have two ninja cards that are shared by everyone.

- Rules
At the beginning of each stage, each player takes cards equal to the number of the stage.

Cards are not played in turn, and each player after waiting for the desired time, plays the lowest card number he has.
In other words, the players must guess what cards are in the hands of the other players so that they can turn their cards in order.

If a card is played, but there is a card with a lower number in the hand of one of the players, it leads to the loss of a heart card, and the cards that had a lower number than the played card are burned and removed from the hands of all players.

Players cannot see each other's hands, but they can see the last card played on the table.

Players must be able to go through the specified steps without losing all of their heart cards.

Players can also choose to use a Ninja card. By using this card, each player plays the smallest card they have.
By doing this, the number of cards of each player is reduced and it gives us an idea about the number of cards in the hands of the other players.
In this case, all the smaller cards remaining in the hands of the players are removed from their hands, but the heart card is not lost.

Players will receive a heart card at the beginning of rounds 3, 6, 9 and a ninja card at the beginning of rounds 2, 5, 8, which is common to all of them.

At the end of the 12th stage, all players will be announced as winners.


general structure

User (client): The way to enter the game is that every user automatically connects to the game server after running.
Each user first announces his name to the server and is added to the lobby. If no other players are present, the user will play the role of host and 
also declare the maximum number of players in the game. Only the host can request the server to start the game.
If there is a game in progress when the user enters the lobby and there is enough space, the user should be able to join it at will.

Server: After the request to start the game by the host user, the server creates a bot and starts the game on the server side, according to the maximum number of players that have been announced and the number of people added to the game. From now on, the server will be the bridge of communication between users and with each new move, it will announce the new state of the game to all players.
Your app should be able to run multiple games simultaneously. That is, after creating a new game, the server adds it to the list of running games.

Bot: Bots have a strategy to play and can play independently. For this purpose, we have designed each bot in such a way that after a certain time it waits,it plays its lowest card.
Note that this waiting time is reset for all bots after each player (human or bot) plays and is measured against the time of the last move. Also, bots do not have the ability to request the use of ninja cards.


- Implementation details
Multiplayer game: In each game, there are a number of players and a number of bots, the sum of which is a fixed amount. In other words, as players increase or decrease, bots take their place or decrease the number of bots.

Authentication: In the game server, after connecting the user, we send a code key to the user that the user sends this key in the AuthToken field in all his messages to the game server. AuthToken is a key for communication between user and server. In fact, this field will be the characteristic of each user, and the server will recognize the user's connection with the AuthToken. When a user logs in again, this value must be generated anew.

- Interface
The console interface is where we update and display the number of remaining cards of each suit (hearts, ninjas, and other players' backs), the player's hand (yours), and the last card played. This interface is displayed on the user (client) side.
For the server, we save important events in a log file.

Reaction:
Players should be able to send emojis to each other during the game. It can be sent by text type or by selecting options. We implemented three of the most used emojis (smiley D:, sad :(, happy :), pokerface :| and ...). The server ignores any textual and numerical content (which is an example of user fraud) and only broadcasts emojis.


- Network of the system:
Your client and server are designed completely separate from each other, so that if the client and server run on two different machines, there will be no problem with the application and both will run correctly.

The communication between the user and the server is done only through the network. The communication between the users and the server will be established through the socket. This connection can be of TCP or UDP type.

The server and the user run separately and read the specified port and address from a specified config file. The user and server configuration files are independent of each other.

In addition, there will be a default port of 8000 and an address of localhost in the program, which will be used if the port and address are not provided by the file.

To connect, it is enough for the server to listen on a specific port, and users can connect to the server by connecting to the server address and that port.
