---
title: A Guide on Save System for Non Linear Games
tag:
- tutorial
- godot
description: this is a written guide on how to build a save system? this is independent
  of which engine you are using
date: '2021-06-03 18:07:17'
---

I have been working 🛠 on a save system for like past few weeks and wasn't able to figure out how to build a save system that save without loosing the previous save file. a.k.a doesn't overwrite save files, just like in Witcher 3. Well unfortunately there were no information available on this topic, including both unreal and unity forum. I did my very own research and brain storming. I come up with few methods to build a save system.

I have made a short **6 min** video on this if you want to see the **Actual result** then you can check out the [YouTube video here](https://www.youtube.com/watch?v=2-jYxB2Hgeo).

<iframe width="560" height="315" src="https://www.youtube.com/embed/2-jYxB2Hgeo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

For the github repo [click here](https://github.com/mayank-prasoon/save-system-template)

Lets get started.

This is a audio version of this blog

<iframe width="100%" height="300" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/1061148178&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe><div style="font-size: 10px; color: #cccccc;line-break: anywhere;word-break: normal;overflow: hidden;white-space: nowrap;text-overflow: ellipsis; font-family: Interstate,Lucida Grande,Lucida Sans Unicode,Lucida Sans,Garuda,Verdana,Tahoma,sans-serif;font-weight: 100;"><a href="https://soundcloud.com/mayank-prasoon-gamedev" title="Mayank Prasoon" target="_blank" style="color: #cccccc; text-decoration: none;">Mayank Prasoon</a> · <a href="https://soundcloud.com/mayank-prasoon-gamedev/how-to-build-a-save-system-for-non-linear-game" title="how to build a save system for non linear game" target="_blank" style="color: #cccccc; text-decoration: none;">how to build a save system for non linear game</a></div>

To understand my point lets look at the problems given below.

# Problems

- **case 01** - The player gets stuck and can't get out of a place.
- **case 02** - The player accidentally triggers a boss fight and can't get out.
- **case 03** - The player buy something from the shop and then realizes that they never needed it.
- **case 04** - The player losses all it's progress due to a silly mistakes.
- **case 05** ⭐ - The player accidentally choose a wrong option in a narrative driven game. (not everyone is good at English 😆)
- **case 06** - The player wants to try out new way or want to experiment with the mechanic but is afraid to loosing the progress.  Killing the whole, try, fail and learn concept.
- _**case 07** - (this is not a huge problem but still worth mentioning) if you have a sibling, cousins or friend you know that they usually come straight to your computer ask to play the game that you were playing. Most of the time they just want to play one specific part of the game._

The are the most common occurrence of problems that can be solved via a non-destructive save system.

## Notable Example

![hollow knight blue lake](https://i.imgur.com/EZn5ZM7.png)

**Hollow Knight** : Hollow Knight is a 2d action-adventure platformer metroidvania souls-like game. filled with tough platforming and difficult combat.
Players have complain that they loses all the progression or they get stuck in one place.

> A YouTuber by the name of Relya mentioned that one of his fan lost 10K geos while exploring. This is a great example of why open world games should have a way to undo the action.

These are some negative reviews of hollow knight on the steam

|  Reviews      |
|----------------|
| ![review 1](https://i.imgur.com/iD25vE7.png)|
| ![review3](https://i.imgur.com/cT5npIq.png) |

The above mentioned reviews have few things in common, the backtracking and the high risk low reward when it comes to exploration.

I completely agree with their points, the game is very punishing. Even when someone is just casually exploring, They can easily get stuck or loose there progress. Many YouTuber (who are well respected in the community have pointed out this problem).

> According to my knowledge of what I have heard, Team Cherry added alot of the stuff in the later stages of the development, like the shade system. So, It is possible that they have initially planned a much smaller map, build the core system for it and then slowly the size was increased. Thus breaking the core design.

> In my personal opinion Hollow Knight is one of the best game that I have ever played and despite its flaws its still a masterpiece. I did't have any good example other than hollow knight.

![subnautica-1021x580](https://i.imgur.com/Pl6jT1L.jpg)

**Subnautica**: Subnautica is a horror survival game. Thing that makes it one of it's kind is the fact that it takes place completely in water.

The game has the same problem as Hollow knight but with a twist. The game does not offer any auto save feature.

It is kind of frustrating, that the game offers a pretty large game area to explore. But have little to no insurance when it come to **save files** and just in case a **fail safe for game breaking bugs**.

|           Reviews            |
|:----------------------------|
|  ![subnautica review](https://i.imgur.com/HbBfPi9.png)  |
| ![subnautica review 2](https://i.imgur.com/hSin1KT.png) |

These are some reviews that I found on the steam page. Most of the negative reviews where same. It talk about the game not having a auto save or the game is buggy.

> If we ignored all these problem it is one of those games that is worth exploring. For me I got this game for free. so, I can't complain.

### Root cause

The problem exist because of the faulty save system and it's destructive nature. You can either make a new save or clear the original one. There is no option for undo.

**How save system looks**

![hollow-knight-select-profile-1920x1080 ](https://i.imgur.com/be6GRc0.jpg)
<p align="center"> <i>Hollow knight</i> </p>

![subnautica ui](https://i.imgur.com/qTVbAMI.png)
<p align="center"> <i>Subnautica</i></p>

---

# Solution

Build and non-destructive save system. Which stores every action of the player.
Lets define some terms

### What is a save system?

A save system is a set of code that save that game data into the storage device of the computer.

> In some games, specially roguelike, the save system is not much important. But in others it is a must have.

### Destructive vs Non-Destructive

> A destructive save system would overwrite the data when ever the player press the save button, where as a non-destructive would not, it act same as the destructive one but does not overwrite the data

You may ask, what makes a non destructive save system better? the answer is simple, "going back in time" to play the specific part of the game.

### Why we need a System like this?

This is to avoid player frustration and a much better way to store a data.

## Examples

### Zelda Breath of the Wild

![310742-zelda-breath-of-the-wild-wallpaper-1920x1080-xiaomi](https://i.imgur.com/LB81EjU.jpg)

Zelda Breath of the wild is one of those game which does not need a non-distructive save system, But still have one, because of its superior open world design it is very easy for the player to get in and out of a confrontation, making it difficult for the player to get stuck or accidentally trigger a boss fight and can't get out of the confrontation. The game has decent amount of verticality so I think it is impossible to get stuck.

![CEMU Screenshot 2021.05.19 - 15.22.23.93](https://i.imgur.com/GD8W2rX.png)

The game saves the data in different save files or something. Each save files is like its own bubble and is completely independent of each other. So you can technically go back in time to play the part if you don't like it. I am not sure how it works but we can make a intelligent guess that it saves the data in multiple files.

### Witcher 3

![the-witcher-3-final-boss-header.png](https://i.imgur.com/bHe8UoU.png)

Witcher 3 also boasts a very large open world with a lot of density and fun encounters all wrapped up in an engaging story. Just like Zelda Breath of the wild, the player can avoid combat.

![The Witcher 3 Screenshot 2021.05.19 - 15.50.25.20.png](https://i.imgur.com/pdE9OGD.png)

The save system is same as the Zelda BoTW but it store very old data (mostly manual saves).

Save system like this can save player a lot of time and headache.

## How can we make a Save System

There are multiple ways to build a save system like this.

### I have come across a few different method of saving data

- Duplication method
- Layering method

 Lets discuss them one by one.

### Duplication Method

In duplication method, a copy of the save file is save in the hard drive. Thus, giving the option to go back in time.

 ✏️ Its like making a copy of text file before erasing it or modifying it.

### Advantages ⬆️

- It is the most simplest and easy to implement.
- Each save file is completely independent of other.
- Great for building a very large game (potentially infinite) and open world. (the save files of minecraft are in gigabaits)
- It is easy to store and backup data.
- Stability and recovery in case there is a game braking bug.
- It does not matter how many save files are there in the game as the game will load one save file at a time

> There is a famous bug in minecraft in which the the game does not properly generates the end dimension. Thus player are not being able to finish the game by beating the Ender Dragon.
> The easiest solution to this problem is to backup the data. This is a great situation to apply the duplication method.

### Disadvantages ⬇️

- It is not meant for narrative game, because of the way the data is stored. (I won't say witcher 3 is an exception but I would say they should have tried other techniques)
- The these system usually act as a fail safe rather than a actual feature. In other words the system works completely independent of the game mechanics and usually don't add any thing to the experience.

#### Real world Example

##### Minecraft

![Base Profile Screenshot 2021.05.19 - 18.09.02.63](https://i.imgur.com/7QqTDlD.png)
Minecraft is a snadbox game made by Notch and currently owned by Microsoft.

You can make backup of your world manually and save them and when ever feel like going back you can do that very easily. This looks very complicated, but it is the only example that I was able to find.

This is done manualy. But still, it's great way to make a low effort save system which is non-destructive in nature.

##### Witcher 3

I'm not sure for certain, that Witcher 3 uses something like the Minecraft.

![witcher 3 save files.png](https://i.imgur.com/T8zsMBr.png)

As you can see the each save is stored in its own file and as the game progresses the size of the file also increases.

For the size and scale of the Witcher 3 this is the possible way to store data.

### Layering Method

In layering method the relative values are stored in the form of layers, (*just a fancy term for arrays*) just like layers in the Krita or Photoshop.

![2021_05_25_03b_Kleki.png](https://i.imgur.com/IlAGAtk.png)

As you can see in the picture there are different layers each layer has a Unique I.D. (for the sake of simplicity we will name them 1, 2, 3...)

- These UID are stored in a array (I call it snapshots). When ever the player press the save button the change get saved in a new layer with a new U.I.D.
- All the different layers are accessed via the descending order of the the U.I.D. generated.
- So then the player decides to go back for some reasons the first U.I.D. at the last get deleted
- The layer of data which we don't need gets disabled rather than getting completely removed.

I know all these sounds like technical jargon. But hear me out, in the end every thing will make sense. I just wanted to show how thing works. and position is something that every game save.

#### Lets understand it with a bit of code

I wrote this in typed GDscript. In this example I'm tring to store the position data of the player the code will record each and every position is possible.

**Important values and Variables**

> The snapshot is array just of the sake of simplsity in the acutual game it will have its own seprate file and contain other info like the date, time, short description, image file location (for the screenshot), a color id, in a dictionary.

So here I am just going to store the position but you can store anything item, attack power or a chain of dialog and choices.

```py
var index_value:int = 3           # sample values, own json file

var snapshot:Array = [0,1,2,3]    # sample values, own json file

var positions:Array = [           # sample values, own json file
 {
  "uid" : 0,
  "position_x": 0,
  "position_y": -40
 },
 {
  "uid" : 1,
  "position_x": 20,
  "position_y": -40
 },
 {
  "uid" : 2,
  "position_x": 10,
  "position_y": -40
 },
 {
  "uid" : 3,
  "position_x": 30,
  "position_y": -40
 },
]
```

**Creates a new snapshot with a unique index value**

```ad-note
runs when the game is saved.
```

```py
func create_new_snapshot() ->void:
 index_value += 1
 snapshot.append(index_value)
 return
```

**Create new layers of data**
This generates new layer of data, The data can be either absolute or relative (but never both at the same time).  

The game will read the layer and returns the absolute value from the relative value example.

```py
func create_new_position_layer() -> void:
 positions.append({
  "uid": snapshot[-1],
  "position_x": position.x,
  "position_y": position.y
  }
 )
 
 return
```

**Load the layers of data**

⭐ By reading the code you might realize that I used absolute value inserted of relative value, in other words the actual co-ordinates instead of the difference between two points, which contradicts my whole idea of layers.

And you know what, You are absolutely right.

The thing is the I can technically add that and it will still work fine but it is tricky to implement and involves alot of math. Lets apply **KISS, Keep It Simple Silly UwU**.

If this was a example of  inventory system, then I would have used the relative values. like `{uid:1, item_name='wood', amount=-5,}` or some thing like that, then it would have been easy to understand.

```py
func load_postion() -> void:
 var temp:Array = []
 
 for x in positions:
  if x["uid"] == snapshot[-1]:
   temp.append(x)
 
 var pos_x:float = temp[-1]["position_x"]    # x postion
 var pos_y:float = temp[-1]["position_y"]    # y postion
 
 position = Vector2(pos_x, pos_y)            # curret position of the sprite 
 return
```

**Delete snapshot, thus by deleting snapshot the layer automatically get disabled**

```py
func delete_snapshot(snapshot_index:int) -> void:
 for _x in range(snapshot_index):
  snapshot.pop_back()
 return
```

**Remove the useless data**

Even though it says that the data is remove it is not is just stored it in a different file

``` ad-warning
The erase method can slow down the code. This block of code requires a bit of work

```

```py
func crush_layers() -> void:
 var temp:Array = []
 var dump:Array=[]
 var temp_snap:Array=snapshot.duplicate()

 
 for x in positions:
  if x["uid"] in temp_snap:
   temp.append(x)
   temp_snap.pop_front()
  else:
   dump.append(x)
 
 positions = temp
 
 var trash:= File.new()
 trash.open("res://trash_save_game.json", File.WRITE)
 trash.store_string(to_json(dump))
 trash.close()
 
 return
```

you can build the save and load system on your own but just in case here are good tutorial.

**Quick tutorial on saving game data**
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/muhC3wJ6wCQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- quick and simple
- uses 3D
- uses the group

**How to save a much more complex game**
<iframe width="560" height="315" src="https://www.youtube.com/embed/WCjoNrPAQcE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- [source code](https://github.com/Ramh5/Tutorials)
- easy and explain the documentation
- uses Group
- slowly explained
- beginner friendly

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/l8ciCkmES1M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Has chapters
- best tutorial 🍓
- a bit difficult to understand if your new.
- long and explain every approach

☄️ **Here how I did it.**

```py
func save() -> void:
 var file:= File.new()
 file.open("res://save_game.json", File.WRITE)
 file.store_string(to_json(positions))
 file.close()
 return

func load_save() -> void:
 var file:= File.new()
 if file.file_exists("res://save_game.json"):
  file.open("res://save_game.json", File.READ)
  var data = parse_json(file.get_as_text())
  file.close()

  positions = data

 else:
  printerr("No saved data!")            # I don't know what this do

 return
```

[original code](https://gdscript.com/solutions/how-to-save-and-load-godot-game-data/) it is borrowed from the site, GDscript.com

#### Advantages ⬆️

- The main advantages is the fact that know data is lost.
- The data is connected in and the game not only load the current save data but also all the previous one.
- Great for narrative driven games and game with branching dialog.
- The inventory, dialog, economy and other systems of the games are easy to build and implement.
- It is possible to store each and everything.

#### Disadvantages ⬇️

- Can have performance penalty if the game is very large.
- Complicated and difficult to manage.
- It possible to go back but not forward again. Just like undo and redo

### Practical Application

The game can be used to store the item inventory.
The game will now be able to store which NPC give the item and properly labeled.

## Distructive vs Layering

| Distructive                                                                                           | Layering                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| How the way the data is stored, (*multiple save files*) only one data of each type is loaded at a time | Since there is only one save file, all the save data of every type of data is loaded at a time                                                |
| The save file are independent to each other                                                           | The save data are related to each other                                                                                                       |
| The file data are usually in absolute value <br> `currentPostion = postion(save_file)`                 | The save data are usually in relative value. <br> `currentPosition = sum_of_relative_postion(save_file)` |
