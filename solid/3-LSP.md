# Para que serve o LSP?
O LSP serve para garantir que uma subclasse possa substituir sua superclasse sem que o comportamento do programa seja alterado. Isso promove a reutilização de código e a flexibilidade do sistema.

# O que ele resolve?
O LSP resolve problemas relacionados à substituição de subclasses. Ele assegura que as subclasses mantenham o comportamento esperado da superclasse, evitando surpresas e bugs quando se trabalha com hierarquias de classes.

# Como aplicar
Vamos considerar um exemplo para ilustrar o LSP. Suponha que temos um sistema de gerenciamento de formas geométricas e queremos calcular a área de diferentes formas.



### Exemplo de código sem LSP

```python 
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def set_width(self, width):
        self.width = width

    def set_height(self, height):
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Rectangle):
    def set_width(self, width):
        self.width = width
        self.height = width

    def set_height(self, height):
        self.height = height
        self.width = height

# Uso das classes Rectangle e Square
def calculate_area(rectangle):
    rectangle.set_width(5)
    rectangle.set_height(4)
    return rectangle.area()

rect = Rectangle(2, 3)
sq = Square(2)

print(calculate_area(rect))  # 20
print(calculate_area(sq))    # 16 (esperado 20, comportamento inesperado)

```

### Dificuldades e problemas
**Comportamento inesperado:** Square não se comporta como Rectangle, quebrando a expectativa de que Square pode substituir Rectangle.

**Confusão de implementação:** As definições de set_width e set_height em Square são confusas e não seguem a mesma lógica da superclasse Rectangle.


### Aplicando LSP

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def set_width(self, width):
        self.width = width

    def set_height(self, height):
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def set_side(self, side):
        self.side = side

    def area(self):
        return self.side * self.side

# Uso das classes Rectangle e Square
def calculate_area(shape: Shape):
    return shape.area()

rect = Rectangle(5, 4)
sq = Square(4)

print(calculate_area(rect))  # 20
print(calculate_area(sq))    # 16

```
### Vantagens e solução

**Comportamento consistente:** Agora, Square e Rectangle implementam a interface Shape de maneira consistente, respeitando o LSP.

**Claridade:** A responsabilidade de cada classe é clara e segue a lógica esperada.

**Substituibilidade:** Tanto Square quanto Rectangle podem ser usados de forma intercambiável onde um Shape é esperado.