# Para que serve o ISP?
O ISP serve para evitar que classes sejam obrigadas a implementar métodos que não precisam, promovendo interfaces mais coesas e específicas.

# O que ele resolve?
O ISP resolve problemas relacionados a interfaces "inchadas" (com muitos métodos) que forçam as classes a implementar métodos desnecessários. Isso resulta em código mais limpo e fácil de manter.

# Como aplicar
Vamos considerar um exemplo para ilustrar o ISP. Suponha que temos um sistema de gerenciamento de tarefas onde algumas tarefas podem ser impressas e outras podem ser digitalizadas.

### Exemplo de código sem ISP

```python
class Task:
    def print(self):
        raise NotImplementedError

    def scan(self):
        raise NotImplementedError

class PrintTask(Task):
    def print(self):
        print("Printing the task")

    def scan(self):
        pass  # Não utilizado, mas precisa ser implementado

class ScanTask(Task):
    def print(self):
        pass  # Não utilizado, mas precisa ser implementado

    def scan(self):
        print("Scanning the task")

# Uso das classes PrintTask e ScanTask
print_task = PrintTask()
scan_task = ScanTask()

print_task.print()  # "Printing the task"
scan_task.scan()    # "Scanning the task"

```

### Dificuldades e problemas


**Métodos desnecessários:** As classes PrintTask e ScanTask são forçadas a implementar métodos que não utilizam.

**Confusão:** O código fica confuso e mais difícil de entender, pois as classes possuem métodos que não fazem sentido para elas.

**Manutenção:** A manutenção do código se torna mais complexa devido à necessidade de implementar métodos não utilizados.


### Aplicando ISP

```python
  from abc import ABC, abstractmethod

class Printable(ABC):
    @abstractmethod
    def print(self):
        pass

class Scannable(ABC):
    @abstractmethod
    def scan(self):
        pass

class PrintTask(Printable):
    def print(self):
        print("Printing the task")

class ScanTask(Scannable):
    def scan(self):
        print("Scanning the task")

# Uso das classes PrintTask e ScanTask
print_task = PrintTask()
scan_task = ScanTask()

print_task.print()  # "Printing the task"
scan_task.scan()    # "Scanning the task"

```

### Vantagens e solução

**Interfaces específicas:** Agora, PrintTask e ScanTask implementam apenas os métodos que realmente utilizam.

**Claridade:** O código é mais claro e compreensível, com classes focadas em suas responsabilidades específicas.

**Manutenção mais fácil:** A manutenção do código é mais simples, pois as classes não são sobrecarregadas com métodos desnecessários.