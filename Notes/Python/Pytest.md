[[Pytest]] is a [[Python]] framework makes it easy to write small, readable tests, and can scale to support complex functional testing for applications and libraries.

```python
def inc(x):
    return x + 1

def test_answer():
    assert inc(3) == 5
```

It is great for : 
- [[Test unitaire|Unit testing]]
- [[Test d’intégration|Integration testing]] 

---

## Key concepts

### Fixtures

A setup that refreshes before each test (ex: create a new instance of a [[Classe|class]], yield a [[Bases de données|database]], ...)

```python
import pytest

class Fruit:
    def __init__(self, name):
        self.name = name
        self.cubed = False

    def cube(self):
        self.cubed = True

class FruitSalad:
    def __init__(self, *fruit_bowl):
        self.fruit = fruit_bowl
        self._cube_fruit()

    def _cube_fruit(self):
        for fruit in self.fruit:
            fruit.cube()

# Arrange
@pytest.fixture
def fruit_bowl():
    return [Fruit("apple"), Fruit("banana")]

def test_fruit_salad(fruit_bowl):
    # Act
    fruit_salad = FruitSalad(*fruit_bowl)

    # Assert
    assert all(fruit.cubed for fruit in fruit_salad.fruit)
```