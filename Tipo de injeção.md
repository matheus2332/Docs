# Injeção de Dependência (DI)

A **Injeção de Dependência** é uma técnica usada para reduzir o acoplamento entre classes. Em vez de uma classe criar instâncias de suas dependências, essas dependências são fornecidas (ou injetadas) por um **container de DI** (ou framework). Isso torna o código mais modular e fácil de testar.

# Comparação entre Transient, Singleton e Scoped

Abaixo está uma tabela comparando os diferentes tipos de **scopes** usados na **injeção de dependência**: **Transient**, **Singleton** e **Scoped**. A tabela detalha as principais características, cenários de uso e diferenças entre eles.

| **Característica**       | **Transient**                                                                                          | **Singleton**                                                                                                 | **Scoped**                                                                                                 |
|--------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| **Instância**            | Nova instância a cada solicitação.                                                                     | Uma única instância compartilhada.                                                                            | Uma instância por escopo (geralmente por requisição HTTP ou unidade de trabalho).                          |
| **Uso Ideal**            | Objetos leves, sem estado compartilhado, ou sem necessidade de manter informações entre as instâncias. | Objetos com estado compartilhado ou que são caros para serem criados repetidamente.                           | Objetos que precisam manter estado durante uma única operação ou requisição, mas não precisam ser globais. |
| **Duração**              | A instância é descartada após cada uso.                                                                | A instância é mantida durante toda a execução da aplicação.                                                   | A instância é mantida durante o escopo de uma operação, geralmente uma requisição ou tarefa.               |
| **Cenário Comum**        | Quando o objeto é leve e não precisa manter um estado entre as invocações.                             | Quando a criação de instâncias é cara e a reutilização é importante (ex: conexão com banco de dados, caches). | Quando o objeto pre do estado.                                                                             |

