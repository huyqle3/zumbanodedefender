Write up for Zumba Fitness's Node Defender at the Ultimate Developer Event 2013
=================
Winston Chen and Huy Le attend the Ultimate Developer Event 2013 and win 1st and 2nd respectively for Zumba Fitness's Node Defender game

https://github.com/zumba/node-defender-game

Defend against waves of murderous server side code that wants nothing more than to kill and disconnect your node client. Node Defender was a websocket game by Zumba Fitness. Created with two servers (Heroku dynos): one for a client server wand a game server, MongoDB for the sessions and game results, and Redis. Browser client was created with Bootstrap 3.0, jade, Sass & Compass, RequireJS, Ace, KinecticJS, and howler.js.

Backstory
=================
Winston and I arrived at the Ultimate Developer Event 2013 on November 21, 2013.Talking with the two people from Zumba Fitness, we learned about their Node Defender game, and we wanted to try to beat the top score and win some prizes. We were to code Javascript instructions for their Node defender and try to win.

Strategy
=================
We started writing code for the event, and testing Node Defender with different instructions. Mainly using conditionals, for loops, and while loops, we tested different scenarios to see what type of attack would be good with certain enemies, how much health each enemy generally had, the probabilities of getting a good hit on certain enemies, etc. At first, I tested certain code with the Node Defender to see how I did. Then, I would change something immediately afterwards to see if a change would be better. However, we realized that although the pattern in how the enemies reacted stayed the same, the organization and the type of enemies changed repeatedly in a pattern that I did not know. Sometimes, code would work well, and other times, code wouldn't work so well despite very specific changes and supposedly good logic. 

Since there was no penalty for repeated submissions, we decided that we should cut out the very specific code, and we should leave a general, simple set of instructions that followed a good logical process that would effectively increase our chances eventually for a high score. 

As a result, we focused on two main approaches for the best general solution to node generator. After looking at the code on github for the node defender and the instructions on how the game was scored, I put priority in first, killing waves as quick as possible to get the 10,000 point boost, and later on, defending myself as long as possible to get most rounds survived and some extra points.

We cut out the fat of the code, created a general, well-working set of instructions for the node defender, and simply, we ran it over and over again until we got high scores.

Scores
=================
winstonc - 147,356
huyle333 - 139,349
aaronjarecki - 138,923

Top Categories
=================
kills - 94 - aaronjarecki
damage - 434 - aaronjarecki
round - 76 - winstonc
waveClears - 8 - winstonc

