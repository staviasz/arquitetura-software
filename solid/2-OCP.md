# Para que serve o OCP?
O OCP serve para aumentar a flexibilidade e a robustez do software, permitindo que ele seja estendido com novas funcionalidades sem risco de quebrar funcionalidades existentes.

# O que ele resolve?
O OCP resolve problemas relacionados à manutenção e evolução do código. Ele evita que alterações em funcionalidades existentes introduzam bugs e permite adicionar novas funcionalidades de maneira segura e eficiente.

# Como aplicar
Vamos considerar um exemplo para ilustrar o OCP. Suponha que temos um sistema de cálculo de descontos, onde queremos aplicar diferentes tipos de descontos a um preço base.

### Exemplo de código sem OCP

```python
class PriceCalculator:
    def __init__(self, base_price):
        self.base_price = base_price

    def calculate(self, discount_type):
        if discount_type == "percentage":
            return self.base_price * 0.9  # 10% de desconto
        elif discount_type == "fixed":
            return self.base_price - 20  # desconto fixo de 20 unidades
        else:
            return self.base_price

# Uso da classe PriceCalculator
calculator = PriceCalculator(100)
print(calculator.calculate("percentage"))  # 90.0
print(calculator.calculate("fixed"))  # 80.0
print(calculator.calculate("none"))  # 100.0

```

### Dificuldades e problemas

**Modificação constante:** Sempre que um novo tipo de desconto é adicionado, a classe PriceCalculator precisa ser modificada.

**Risco de introduzir bugs:** Modificar o código existente pode introduzir bugs em funcionalidades já existentes.

**Escalabilidade:** Adicionar novos tipos de descontos pode tornar o método calculate grande e complexo.

### Aplicando OCP

```python
from abc import ABC, abstractmethod

class DiscountStrategy(ABC):
    @abstractmethod
    def apply_discount(self, base_price):
        pass

class PercentageDiscount(DiscountStrategy):
    def apply_discount(self, base_price):
        return base_price * 0.9  # 10% de desconto

class FixedDiscount(DiscountStrategy):
    def apply_discount(self, base_price):
        return base_price - 20  # desconto fixo de 20 unidades

class NoDiscount(DiscountStrategy):
    def apply_discount(self, base_price):
        return base_price  # sem desconto

class PriceCalculator:
    def __init__(self, base_price, discount_strategy: DiscountStrategy):
        self.base_price = base_price
        self.discount_strategy = discount_strategy

    def calculate(self):
        return self.discount_strategy.apply_discount(self.base_price)

# Uso da classe PriceCalculator com diferentes estratégias de desconto
base_price = 100

percentage_calculator = PriceCalculator(base_price, PercentageDiscount())
fixed_calculator = PriceCalculator(base_price, FixedDiscount())
no_discount_calculator = PriceCalculator(base_price, NoDiscount())

print(percentage_calculator.calculate())  # 90.0
print(fixed_calculator.calculate())  # 80.0
print(no_discount_calculator.calculate())  # 100.0

```

### Vantagens e solução
**Extensibilidade:** Novos tipos de descontos podem ser adicionados sem modificar o código existente.

**Redução de risco:** Adicionar novas funcionalidades não afeta as funcionalidades existentes, minimizando a introdução de bugs.

**Manutenção mais simples:** Cada classe de estratégia de desconto é pequena, focada e mais fácil de manter.