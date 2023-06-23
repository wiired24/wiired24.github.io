---
title: Game Dev with Godot 4 - Part 3
image: "https://godotengine.org/assets/press/icon_color.png"
date: 2023-06-23 11:05:00 -500 
categories: [general]
tags: [general]
---

## Scripting with GDScript
Games comes down to two things art and logic. There is a lot that happens under the hood with Godot that the engine takes care of for you, however you as the developer are still left with a world of possibilities when it comes to scripting behaviors in your Godot Games. Fear not though. GDScript is very straightforward and a joy to use. If you have never programmed before  I would recommend taking a few hours to learn the basics of Python which is very similar to GDScript syntax wise, then come back to this tutorial. 

## What we will be building today
The goal for this tutorial is to build a basic gameplay mechanic whereby when a timer reaches zero the game over screen that we made in the last tutorial is triggered. As you can imagine this might be a mechanic that you would even use in your own Godot Games. Let's get started then. In the Godot Editor towards the top center there should be a + icon. Click on that. Here you will now be able to create a new node. Go ahead and create a 2D Scene and rename it to game. Up at the top left panel where you see Scene, Project, Debug, etc select Scene and in the dropdown menu make sure to select "Save Scene as". Lastly, select save. 

## Adding the Timer Node
I mentioned we are implementing a basic game mechanice whereby when time reaches zero the game over screen is triggered. In order for us to do that we will need to add a timer node in our scene. Go ahead and right click on the game node and select "Add Child Node". Type in "Timer" to the search box and select it through. Take a look over at the inspector on the right side. Do you see how there is a wait time property? Go ahead and set that to 10 seconds and then hit enter to confirm the change. Pro tip: you can either drag the slider across or you can simply click into the box and then set it. I personally find the latter to be easier but it's up to you. Now tick the box that says "Autostart" just below where you set the time. This way our timer will automatically begin. 


## Your first Script in Godot
It is now time to go ahead and add a script to our game. Right click on game and select "Attach Script". A pop up will appear asking if you'd like to name your script game.gd. Click Create. Once you have created your script you will see two functions 

```gdscript
func _ready():
  pass
```
```gdscript
func _process(delta):
  pass
```
The ready function is called right away and would typically include anything we want to happen initially. The _process(delta) function takes care of logic that needs to happen every frame. If you don't understand that right now don't worry about it. Things will click more as we continue to work with GDScript. Now that we have our script created let's wire it up.  

## Wiring it up
Now that we have our Timer Node in the scene and we have set the time we need to connect it to our script that we just made. Click on the Timer Node and over in the inspector panel switch the tab to "Node". Do you see where it says timeout()? This is a function that can be connected to our game script. That's exactly what we are looking for! Go ahead and right click it. Now select connect. A pop up will appear asking where you would like to connect the timeout function. The game script should be auto selected by default but if it's not then go ahead and select it and hit connect. You should now see that in the game script we now have 

```gdscript
func _on_timer_timeout():
	pass # Replace with function body.
```

## Switching Scenes
The last thing we need to do is implement some logic that says "Hey after 10 seconds has run out let's switch to game over". The first part we already handled through Godot when we set our timer. Now we just need to handle the scene switching logic. This can be done quite easily using the change_scene_to_file function. In your _on_timer_timeout remove the line that says pass # Replace with function body. Now in order to change the to the game over scene after the timer ends we need to add this piece of code to our script.

```gdscript
func _on_timer_timeout():
	get_tree().change_scene_to_file("res://game_over.tscn") 
```
We're almost done! One of the last things we need to do is set our game scene as the main scene so once the project is loaded it will start at our game scene and then once the timer runs out, transition over to the game over scene. Bottom left side of the editor under the "FileSystem" tab, right-click on game.tscn and select "Set as Main Scene". Now click the play button and if everything goes well within 10 seconds you should see the blank game scene change to the game over scene. Congratulations you just implemented your first custom piece of logic in Godot! 🎉


## Coming up next
We still have a lot to cover in this series. We've barely scratched the surface of what we will need to implement to make this into any sort of a "real" game. I'm intentionally writing this series in such a way that it is easy to understand and brown down into small parts, rather than introducing too much too fast. In the next tutorial we will look at implementing a fairly basic HUD that displays the countdown timer in the scene so you can see it countdown to zero before the game ends. Then we will work on adding a tilemap to our game, building out a level and putting a player into our game. After that we will look at making it so that the player has x amount of coins to collect and if he fails to collect all of them before the timer reaches zero then the game will end. We will add custom sound effects, and maybe even throw in a credits scene. This will be a fairly basic game but you will learn alot about the fundamentals of working with Godot and game development in general. I'm expecting to get the next release out within a week or two. Best of luck on your game dev journey, see you then. 