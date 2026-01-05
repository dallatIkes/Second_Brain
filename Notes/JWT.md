# [[JSON]] WEB [[Token]]

**We create the token**
```python
jwt.encode(
	{DATA, EXP},
	SECRET,
	ALGO
)

# DATA : {"sub": "samy"}
# EXP : datetime + Δt
# SECRET : cryptographic signature (used to make sure that it's really the server that created this token and that it's not forged (real-life analogy : stamp on the wristband))
```
**The token is send via the header by the [[Client|client]] and then decoded by the [[Serveur|server]]** 
```python
jwt.decode()
```