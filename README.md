# Symphony of Survival

![demo](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExeHE5bXYxajY5bmNjemsxZWRzaHpwM20wZGl0ODJpdDR3emRzdWdmOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/zZh10sHYh5QBRvRQwe/giphy.gif)

A rhythm game about surviving the cycle of answering calls and writing emails as a
salaryman. Play on [itch](https://ellenlowing.itch.io/symphony-of-survival)!

## Gameplay
Gameplay is similar to Taiko no Tatsujin, but the beats are spawned in a circle rather than on a straight line.

Hit left arrow key [←] for green color type beat. 
Hit right arrow key [→] for blue color type beat. 
Hold either key for yellow color type beat.

## Programming
To spawn beats in sync with the music, you need to keep track of the song position in beats. To obtain that, you get the current time of the audio system in seconds and convert it to beats using the provided BPM of song.

A simple array is enough to store beat information that is parsed from a beatmap. Each beat has 2 variables: 1) color/type of beat and 2) song position in beats. In each update loop, if the current song position is greater than the next beat to spawn in beats, generate the beat in the cycle.

Since the beats are spawned in a circle, where each full cycle represents a bar of 4 beats, you simply use parametric equations to calculate the angle and hence the position at which a beat should be spawned, given its beat position in bar. 

The main player and beat objects both have a collider component. Once they start colliding, the beat is activated and starts detecting keyboard inputs for hits. When a hit is detected, the difference in angle between the two objects will be used to determine the performance of the hit (early, great, perfect, late). The beat is considered a miss if the player doesn't hit in time before it is deactivated. 

A health bar and score system are implemented to monitor overall performance. The game keeps going as long as health is nonzero. It takes damage when a note is missed and gains health for a great or perfect beat hit. The score gets incremented by different degrees depending on the hit performance.


## Resources
[Coding to the Beat - Under the Hood of a Rhythm Game in Unity](https://www.gamedeveloper.com/audio/coding-to-the-beat---under-the-hood-of-a-rhythm-game-in-unity)
