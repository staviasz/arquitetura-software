# Para que serve o SRP?
O SRP sugere que uma classe deve ter apenas uma razão para mudar, ou seja, deve ter apenas uma responsabilidade. Isso facilita a manutenção e a evolução do código, pois mudanças em uma responsabilidade não afetam outras responsabilidades.

# O que ele resolve?
O SRP resolve problemas de acoplamento e coesão. Quando uma classe tem múltiplas responsabilidades, é mais provável que mudanças em uma responsabilidade afetem outras partes do código, introduzindo bugs e dificultando a manutenção. O SRP ajuda a evitar isso, promovendo classes mais focadas e menos propensas a mudanças inesperadas.

# Como aplicar
Vamos considerar um exemplo para ilustrar o SRP. Suponha que temos uma classe Report que tem responsabilidades de geração de relatórios e também de envio de emails. Esse é um exemplo clássico de violação do SRP.

### Exemplo de código sem SRP

```python
class Report:
    def generate(self, data):
        # Gera o relatório a partir dos dados
        report = f"Relatório: {data}"
        print(report)
        return report

    def send_email(self, report, email):
        # Envia o relatório por email
        print(f"Enviando relatório para {email}")
        # código para envio de email
        print("Relatório enviado com sucesso.")

# Uso da classe Report
report = Report()
relatorio = report.generate("Dados de exemplo")
report.send_email(relatorio, "exemplo@dominio.com")

```

### Dificuldades e problemas

**Acoplamento:** A classe Report está acoplada a duas responsabilidades distintas: geração de relatórios e envio de emails.

**Manutenção:** Se precisar alterar a forma como os emails são enviados, teremos que modificar a classe Report, correndo o risco de introduzir bugs na geração de relatórios.

**Testabilidade:** Testar a geração de relatórios independentemente do envio de emails é mais difícil.

### Exemplo de código com SRP

```python
class ReportGenerator:
    def generate(self, data):
        # Gera o relatório a partir dos dados
        report = f"Relatório: {data}"
        print(report)
        return report

class EmailSender:
    def send_email(self, report, email):
        # Envia o relatório por email
        print(f"Enviando relatório para {email}")
        # código para envio de email
        print("Relatório enviado com sucesso.")

# Uso das classes separadas
report_generator = ReportGenerator()
email_sender = EmailSender()

relatorio = report_generator.generate("Dados de exemplo")
email_sender.send_email(relatorio, "exemplo@dominio.com")

```
### Vantagens e solução

**Desacoplamento:** Agora, ReportGenerator e EmailSender têm responsabilidades únicas e bem definidas.

**Manutenção:** Alterações na lógica de envio de emails não afetam a geração de relatórios e vice-versa.

**Testabilidade:** Podemos testar cada classe de forma independente, facilitando a detecção de bugs e a manutenção do código.