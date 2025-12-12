[[Godot]] icon : ![[CharacterBody2D.svg]]
[Official documentation](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)

**CharacterBody2D** is a specialized class for physics bodies that are meant to be user-controlled. They are not affected by physics at all, but they affect other physics bodies in their path. They are mainly used to provide high-level API to move objects with wall and slope detection ([move_and_slide](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html#class-characterbody2d-method-move-and-slide) method) in addition to the general collision detection provided by [PhysicsBody2D.move_and_collide](https://docs.godotengine.org/en/stable/classes/class_physicsbody2d.html#class-physicsbody2d-method-move-and-collide). This makes it useful for highly configurable physics bodies that must move in specific ways and collide with the world, as is often the case with user-controlled characters.

Has no initial shape so don't forget to add a [[CollisionShape2D]] child.

## Properties

- velocity : Vector2

## Methods

- move_and_slide()