# [[Programmation Orientée Objet|OOP]]

**"Favor Composition over [[Héritage|Heritage]]"**

Relations entre [[Classe|classes]] :
- **is-a :** [[Héritage]]
- **has-a :** Composition

# Code Smell

- Long [[Méthode|method]]
- Large [[Classe|class]]/God [[Classe|class]]
- Duplicated Code
- Dead Code
- Feature Envy

# SOLID

## Single Responsibility

Une [[Classe|classe]] ne devrait avoir qu'une seule responsabilité

```python
# VIOLATION SRP : 2 responsabilites
class Device:
	def __init__(self, device_id, name):
		self.device_id = device_id
		self.name = name

	def turn_on(self):
		# Responsabilite 1 : Logique metier
		self.status = "ON"

	def save_to_database(self):
		# Responsabilite 2 : Persistence (VIOLATION !)
		db.execute(f"INSERT INTO devices VALUES ...")
```
## Open-Closed

Les entités logiques doivent être ouvertes à l'extension mais fermées à la modification

```python
# VIOLATION OCP : Modification a chaque nouveau type
class DeviceController:
	def control (self, device_type, action):
		if device_type == "light":
			# Logique lumiere
			pass
		elif device_type == "thermostat":
			# Logique thermostat
			pass
		elif device_type == "camera":
			# Logique camera (modification !)
			pass
		# Pour chaque nouveau type, on modifie cette methode !
```
## Liskov Substitution

Les objets d'une [[Classe|classe]] dérivée doivent pouvoir remplacer les objets de la [[Classe|classe]] de base sans altérer le comportement du programme

```python
# VIOLATION LSP : Carre herite de Rectangle
class Rectangle:
	def set_width(self, w):
		self.width = w

	def set_height(self, h):
		self.height = h

class Square(Rectangle): # VIOLATION LSP !
	def set_width(self, w):
		self.width = w
		self.height = w # Force hauteur = largeur

	def set_height(self, h):
		self.width = h
		self.height = h
```

```python
# Probleme :
rect = Square()
rect.set_width(5)
rect.set_height(10)
# Attendu : width=5, height=10
# Reel : width=10, height=10 (VIOLATION !)
```
## Interface Segregation

Les clients ne doivent pas être forcés à dépendre d'interfaces qu'ils n'utilisent pas 

```python
# VIOLATION ISP : Interface trop large
class IDevice(ABC):
	@abstractmethod
	def turn_on(self): pass

	@abstractmethod
	def turn_off(self): pass

	@abstractmethod
	def read_value(self): pass # Pas pour tous !

	@abstractmethod
	def set_temperature(self): pass # Seulement thermostats !

	@abstractmethod
	def take_picture(self): pass # Seulement cameras !
```
## Dependency Inversion 

Les modules de haut niveau ne doivent pas dépendre des modules de bas niveau

```python
# VIOLATION DIP : Dependance concrete
class DeviceService:
	def __init__ (self):
		# Couplage fort a SQLRepository
		self.repo = SQLRepository() # VIOLATION !

	def save_device(self, device):
		self.repo.save(device)

class SQLRepository:
	def save(self, device):
		# SQL logic
		pass

# Problème : Impossible de changer la DB sans modifier DeviceService
```

