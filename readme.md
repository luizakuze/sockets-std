# Diagrama de sequência do protocolo

## Conceitual

```mermaid
---
config:
    sequence:

    mirrorActors: false
---
sequenceDiagram
autonumber
    participant C as Cliente
    participant S as Servidor

    C ->> S: Conexão
    S ->> C: Mensagem de conexão
    loop Pedido != Sair
        S ->> C: Acão (Desligar/Ligar)
        C ->> S: Resposta (Desligado/Ligado)
    end
```

## Implementação
```mermaid
---
config:
    sequence:
    mirrorActors: false
---
sequenceDiagram
autonumber
    participant C as Cliente
    participant S as Servidor

    C ->> S: Conexão
    create participant T as Thread
    S ->> T: Cria
    T -->> C: 
    S ->> C: Mensagem de conexão
    loop Pedido != Sair
        S ->> C: Ação (Desligar/Ligar)
        C ->> S: Resposta (Desligado/Ligado)
    end
    S ->> T: Finaliza
    S ->> C: Mensagem de fim
```
## Descriçao

Caso exista mais clientes, entao a o Servidor criara mais threads com as mesmas acoes descritas.

1. **Cliente** solicita conexao com o servidor 

1. **Servidor** Cria a thread

1. **Thread** Conecta com o cliente

1. **Servidor** responde que esta conectado com o cliente

1. **Açao** do servidor no cliente desliga ou liga o iot client

1. **Cliente** responde seu estado atual ou seja se esta ligado ou desligado

1. Apos receber a mensagem sair o servidor finaliza a **thread** 

1. **Servidor** diz que esta desconectando ao cliente
