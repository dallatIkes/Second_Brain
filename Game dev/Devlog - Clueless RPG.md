# 03/08/2024

I created a new [[Godot]] project. The idea is to create a little RPG game inspired by [Crashlands](https://store.steampowered.com/app/391730/Crashlands/), [Vrising](https://store.steampowered.com/app/1604030/V_Rising/) and [Stardew Valley](https://store.steampowered.com/app/413150/Stardew_Valley/). It will basically be a pixel art survivor game with a RPG dimension.

Here is what I did today:
- I created a ``Game dev`` directory in my obsidian vault and created some notes about the major 2D Nodes I'll use during this project.
- I created a player scene and made it move with a [[CharacterBody2D]]
```gdscript
extends CharacterBody2D

@export var speed = 500

func get_input():
	return Input.get_vector("left", "right", "up", "down").normalized()

func _process(_delta):
	velocity = get_input() * speed
	move_and_slide()
```
- I created a tree scene and made it detect is the player is nearby with an [[Area2D]]
```gdscript
extends Area2D

@onready var player = get_node('/root/Game/Player')

func _process(_delta):
	if player in get_overlapping_bodies():
		print('The player entered the area!')
```
This code works but is not optimized (it breaks if we move the player node in the game tree for example) so I need to fix it, plus I need to learn about signals in order to send one to the player when the tree detects him in its area. 

#TODO Lean about [[Godot]] signals

# 04/08/2004

I fixed the problem with signals:

Tree script
```gdscript
extends Area2D

# The player enters the gathering zone
func _on_body_entered(body):
	if(body.name == 'Player'):
		body.add_tree(self.get_parent())

# The player exits the gathering zone		
func _on_body_exited(body):
	if(body.name == 'Player'):
		body.remove_tree(self.get_parent())
```

Player code
```gdscript
extends CharacterBody2D 

var near_trees = []

func add_tree(tree: Node2D):
	near_trees.append(tree)
	
func remove_tree(tree: Node2D):
	near_trees.erase(tree)
func _process(delta):
	print(near_trees)
	if Input.is_action_pressed("interact"):
		for tree in near_trees:
			tree.queue_free()
```

This works pretty well but I think that for the player animation (chopping wood, attacking enemies, etc...), it's better to create an [[Area2D]] around the player (that moves according to the side the player is facing) and to detect if something is in it.

#TODO Learn how to change a [[CollisionShape2D|CollisionPolygon2D]] shape with code. The idea is to change the [[Area2D]] position and rotation according to the player's facing direction.
![[Pasted image 20240805001105.png]]

I also added the delta argument in the move function for the character, which makes the movement mush smoother. 
#Note that I had to considerably increase the speed value (because delta which is the time elapsed between two frames is very small) and because it is a ``@export var`` it's value in the player scene is not linked to its value in the game scene.
```gdscript
func move(delta):
	velocity = get_input() * speed * delta
	move_and_slide()
```

# 05/08/2004

I added an [[Area2D]] to my player with a [[CollisionShape2D|CollisionPolygon2D]] in a triangle shape that I called AOE
![[Pasted image 20240805220347.png]]

#Note AOE is now used to detect ressources in it, but it may be used as a damage zone for spells.

I change its rotation according to the player's direction
```gdscript
# Player's Area Of Effect
@onready var AOE = $Area2D/CollisionPolygon2D

# Updates the AOE according to the player's direction
func update_AOE() -> void:
	if Input.is_action_pressed("left"):
		AOE.rotation_degrees = -90
	if Input.is_action_pressed("right"):
		AOE.rotation_degrees = 90
	if Input.is_action_pressed("up"):
		if Input.is_action_pressed("right"):
			AOE.rotation_degrees = 45
		elif Input.is_action_pressed("left"):
			AOE.rotation_degrees = -45
		else:
			AOE.rotation_degrees = 0
	if Input.is_action_pressed("down"):
		if Input.is_action_pressed("right"):
			AOE.rotation_degrees = 135
		elif Input.is_action_pressed("left"):
			AOE.rotation_degrees = -135
		else:
			AOE.rotation_degrees = 180
```
I then added the same signals used by the tree's [[Area2D]] (that I now removed)
```gdscript
# Gatherable ressource enters AOE
func _on_area_2d_body_entered(body: Object) -> void:
	if(body.is_in_group('Ressources')):
		add_ressource(body)
		print('Added %s' % body.name)

# Gatherable ressource exits AOE
func _on_area_2d_body_exited(body: Object) -> void:
	if(body.is_in_group('Ressources')):
		remove_ressource(body)
		print('Removed %s' % body.name)
```
I added a group called Ressources to be able to use the player's AOE and these methods with many other scenes (like minerals or other gatherable ressources)

After that I added a gather method to the trees
```gdscript
@export var durability = 100

# Gathering mechanic : durability decreases until ressource is destroyed
func gather() -> void:
	print('Gathering ressource...')
	durability -= 25
	print('Durability : %d/100' % durability)
	if durability <= 0:
		queue_free()
		print('Ressource destroyed!')
```
and a gather method to the player
```gdscript
# Gathers all the ressources in the player's range
func gather() -> void:
	for ressource in near_ressources:
			ressource.gather()
```

I learned about inherited scenes. First we need to create a scene, here I created the item scene
![[Pasted image 20240806000231.png]]
```gdscript
extends Node

func print_stats() -> void:
	print('===')
	print('Name : %s' % name)

```

#Note New inherited scene shortcut : Ctrl+Shift+N

Then I create a new inherited scene and I choose the item scene as parent
![[Pasted image 20240806000214.png]]
Here we notice that the new tool scene inherits everything from the item scene : its nodes and script. Inherited nodes are good (we want all our items to have [[Sprite2D]] including tools), but we don't want the same super script. So we detach the item script from the tool scene and we create its own script but we make it inherit from the tool one
```gdscript
extends "res://scripts/item.gd"

@export var dmg: int
@export var max_durability: int
@export var current_durability: int

func print_stats() -> void:
	super.print_stats()
	print('Durability : %d/%d' % [current_durability, max_durability])

func _ready():
	name = "Woodcuter's axe"
	max_durability = 100
	current_durability = 89	
	print_stats()
```
We notice that we can call the super scene methods with the ``super`` attribute.

#TODO Complete the item and tool class and create a first tool (an axe for example) and make it usable (the axe will be more efficient for cutting wood which means that the gather method will probably take a tool as argument to consider its damage)

# 06/08/2004

I implemented new classes
```gdscript
extends Node
class_name item

@export var item_name: String

func _init(_item_name: String = "item"):
	name = _item_name
	item_name = name

func print_stats() -> void:
	print('===')
	print('Name : %s' % name)
```

```gdscript
extends item
class_name tool

@export var dmg: int
@export var max_durability: int
@export var current_durability: int

func _init(tool_name: String = "tool", tool_max_durability: int = 0, tool_dmg: int = 0):
	super._init(tool_name)
	max_durability = tool_max_durability
	current_durability = tool_max_durability
	dmg = tool_dmg

func print_stats() -> void:
	super.print_stats()
	print('Damage : %d' % dmg)
	print('Durability : %d/%d' % [current_durability, max_durability])
```

```gdscript
extends tool
class_name axe

func _init():
	super._init('Axe', 100, 10)
	print_stats()
```

In the game tree scene, i added a new scene : axe

I also added an ``equiped_tool`` exported variable to the player scene
```gdscript
# Player's equiped tool
@export var equiped_tool: tool
```
so i can drag the tool in the inspector

It works well, the only issue is that the axe stats don't appear in the [[Godot]] inspector
![[Pasted image 20240806235230.png]]

#TODO Watch this video to learn more about classes to eventually find a better implementation
![](https://youtu.be/uV6XIlLmMco)

# 07/08/2024

I learned a little bit more about [[Godot]] classes and exported values. I took the decision to abort the axe class and its code and instead create a new scene using the tool node in order to change its property values in the inspector and then add it as a node in the game scene tree.

#TODO Figure out a way to load an item sprite and make the axe sprite follow the player and launch a little animation when it's used (I already put the axe's gravity center at the stick end so the animation will be a simple rotation of the sprite)
![](https://youtu.be/roSsChfW1P8)

#TODO Learn about the [[Ressource]] class
![](https://www.youtube.com/watch?v=vzRZjM9MTGw&pp=ugMICgJmchABGAHKBQ9nb2RvdCByZXNzb3VyY2U%3D)

![](https://www.youtube.com/watch?v=TGdQ57qCCF0&pp=ugMICgJmchABGAHKBQ9nb2RvdCByZXNzb3VyY2U%3D)

# 08/08/2024

I figured out how [[Ressource|Ressources]] work. First I create a script extending from [[Ressource]]
```gdscript
extends Resource
class_name Item

@export var name: String
@export_multiline var description: String
@export var dmg: int
@export var current_durability: int
@export var max_durability: int
@export var sprite: Texture2D
```
It's a way of serializing objects, here items.

Then we create a new [[Ressource]] based on this script and we fill its properties
![[Pasted image 20240808230034.png]]

After that, we can create a new scene to instantiate this item
```gdscript
extends Sprite2D
class_name Axe

@export var stats: Item

# Temporary axe animation
func animate():
	for angle in range(0, 50, 10):
		rotation_degrees = angle
		await get_tree().create_timer(0.01).timeout 

func _ready():
	scale = Vector2(3, 3)
	position = Vector2(100, 0)
	texture = stats.sprite
```
![[Pasted image 20240808230851.png]]

Finally, I just need to add it in the main game scene tree (as our player child for more convenience)
![[Pasted image 20240808231008.png]]

#TODO Tidy up the project file organization and clean the scripts