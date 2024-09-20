[[Godot]] icon : ![[Area2D.svg]]
[Official documentation](https://docs.godotengine.org/en/stable/classes/class_area2d.html)

Area2D is a region of 2D space defined by one or multiple [[CollisionShape2D]] or CollisionPolygon2D child nodes. It detects when other [[CollisionObject2D]]s enter or exit it, and it also keeps track of which collision objects haven't exited it yet (i.e. which one are overlapping it).

Use example : create a zone with a different gravity, music, etc...

## Methods

- has_overlapping_bodies()