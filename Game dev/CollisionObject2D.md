[[Godot]] icon : ![[Object.svg]]
[Official documentation](https://docs.godotengine.org/en/stable/classes/class_collisionobject2d.html)

Abstract base class for 2D physics objects. CollisionObject2D can hold any number of Shape2Ds for collision. Each shape must be assigned to a shape owner. Shape owners are not nodes and do not appear in the editor, but are accessible through code using the ``shape_owner_*`` methods.