[[Godot]] icon : ![[Node2D.svg]] 
[Official documentation](https://docs.godotengine.org/en/stable/classes/class_node2d.html)

A 2D game object, with a transform (position, rotation, and scale). All 2D nodes, including physics objects and sprites, inherit from Node2D. Use Node2D as a parent node to move, scale and rotate children in a 2D project. Also gives control of the node's render order.

## Properties

- global_position : Vector2
- global_rotation : float
- global_scale : Vector2

## Methods

- move_local_x(float delta, bool scaled=false)
- move_local_y(float delta, bool scaled=false)
- rotate(float radians)
- apply_scale(Vector2 ratio)



