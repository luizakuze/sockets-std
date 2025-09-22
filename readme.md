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
    T ->> C: Mensagem de conexão
    loop Pedido != Sair
        T ->> C: Ação (Desligar/Ligar)
        C ->> T : Resposta (Desligado/Ligado)
    end
    S ->> T: Finaliza

```
## Descriçao

Caso exista mais clientes, entao a o Servidor criara mais threads com as mesmas acoes descritas.

1. **Cliente** solicita conexao com o servidor 

1. **Servidor** Cria a thread

1. **Thread** Conecta com o cliente

1. **Thread** responde que esta conectado com o cliente

1. **Açao** da Thread no cliente desliga ou liga o  cliente

1. **Cliente** responde seu estado atual ou seja se esta ligado ou desligado

1. Apos receber a mensagem sair o servidor finaliza a **thread** 


