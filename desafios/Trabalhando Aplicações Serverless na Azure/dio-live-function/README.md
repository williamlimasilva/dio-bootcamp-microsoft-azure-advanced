# Aplicações Serverless na Azure

As aplicações serverless na Azure permitem que você execute código sem precisar gerenciar explicitamente a infraestrutura do servidor. Com o Azure Functions, você pode desenvolver funções que são acionadas por eventos, como alterações em dados, solicitações HTTP, mensagens de fila e muito mais. As principais vantagens das aplicações serverless incluem:

- **Escalabilidade automática**: As funções são escaladas automaticamente com base na demanda.
- **Pagamento por execução**: Você paga apenas pelo tempo de execução do seu código.
- **Desenvolvimento rápido**: Foco no código e na lógica de negócios, sem se preocupar com a infraestrutura.

## Descrição

Este projeto contém uma série de Azure Functions, cada uma com um propósito específico. Abaixo está uma descrição de cada função:

## Funções

### fn-intput-blob

Esta função do Azure é acionada por um blob no contêiner `samples-workitems`. Ela lê o conteúdo do blob e grava um novo blob no contêiner `output` com o mesmo nome e sufixo "-output.txt".

### fn-ler-sb

Esta função do Azure é acionada por uma mensagem em uma fila do Service Bus chamada "logicapp". Ela lê o corpo da mensagem, que é presumido ser JSON, e tenta enviá-lo para uma URL externa. Se o envio for bem-sucedido, a mensagem é concluída; caso contrário, a mensagem é adiada.

### fn-save-sql

Esta função do Azure é acionada por uma requisição HTTP POST para a rota "PostFunction". Ela lê o corpo da requisição, deserializa-o em um objeto `ToDoItem`, gera um novo ID para o item, define uma URL e insere o item em uma tabela de banco de dados SQL chamada "dbo.ToDo".

### fn-simples

Esta função do Azure é acionada por uma requisição HTTP GET ou POST. Ela simplesmente retorna a mensagem "Welcome to Azure Functions!".

### fn-tempo

Esta função do Azure é acionada por um timer a cada 5 segundos. Ela registra a hora atual e o próximo agendamento do timer.
