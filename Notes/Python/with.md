In [[Python]] `with` automatically 
- opens
- uses
- closes
a ressource (and this even if an error occurs)

---

For example :
```python
with open("file.txt") as f:
    data = f.read()
```
is the same as :
```python
f = open("file.txt")
try:
    data = f.read()
finally:
    f.close()
```
