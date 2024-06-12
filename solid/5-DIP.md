# Para que serve o DIP?
O DIP serve para reduzir o acoplamento entre módulos de um sistema, permitindo que módulos de alto nível (aqueles que contêm a lógica de negócio) não sejam diretamente dependentes de módulos de baixo nível (aqueles que implementam detalhes técnicos). Isso facilita a manutenção e a escalabilidade do sistema.

# O que ele resolve?
O DIP resolve problemas relacionados ao acoplamento direto entre módulos de alto nível e módulos de baixo nível. Sem o DIP, mudanças em módulos de baixo nível podem forçar alterações nos módulos de alto nível, tornando o sistema frágil e difícil de manter.

# Como aplicar
Vamos considerar um exemplo para ilustrar o DIP. Suponha que temos um sistema que envia notificações por email.

### Exemplo de código sem DIP

```python
class EmailSender:
    def send_email(self, message, recipient):
        # Lógica para enviar email
        print(f"Enviando email para {recipient}: {message}")

class Notification:
    def __init__(self, email_sender):
        self.email_sender = email_sender

    def notify(self, message, recipient):
        self.email_sender.send_email(message, recipient)

# Uso das classes Notification e EmailSender
email_sender = EmailSender()
notification = Notification(email_sender)

notification.notify("Olá, mundo!", "exemplo@dominio.com")

```

### Dificuldades e problemas

**Dependência direta:** A classe Notification depende diretamente da classe EmailSender, criando um acoplamento forte.

**Dificuldade para testar:** Para testar Notification, é necessário utilizar uma instância real de EmailSender, complicando os testes.

**Flexibilidade limitada:** Se quisermos mudar a forma de enviar notificações (por exemplo, para SMS), precisaríamos modificar a classe Notification.