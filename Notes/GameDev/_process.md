```gdscript
@export var speed = 400

func _process(delta):
	var input_direction = Input.get_vector("left", "right", "up", "down")
	velocity = input_direction * speed
	move_and_slide()
```

\_process is a native [[Godot]] function that runs at every frame. It takes a delta parameter which is the time difference between the current frame and the previous one (in seconds). This argument is very important because it lets us make motion time-dependent rather than frame-dependant which means that our game will be the same on all computers. To do so we use a formula to go from time (delta) to the distance we wich to move (speed, angular speed, etc...)