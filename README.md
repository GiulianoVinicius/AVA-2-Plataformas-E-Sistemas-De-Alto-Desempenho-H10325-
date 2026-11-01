# AVA-2 - Plataformas e Sistemas de Alto Desempenho (H10325)

Este repositório contém uma demonstração prática de conceitos fundamentais de sistemas distribuídos e comunicação entre processos, implementada em Python usando apenas a biblioteca padrão.

## Objetivo

O projeto explora tópicos estudados em uma AVA (atividade de validação de aprendizagem), com foco em:

- RPC (Remote Procedure Call)
- Registro de nomes / descoberta de serviços
- Barreiras de sincronização
- Relógios lógicos (Lamport e vetorial)
- Eleição Bully
- Quórum de maioria para votação

## Arquivo principal

O código principal está no arquivo:

- `código`

O próprio arquivo contém instruções de execução em Python, como por exemplo:

```bash
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py"
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py" --modo rpc
```

## Estrutura do código

### 1. RPC com XML-RPC
O script cria um servidor XML-RPC e registra um serviço de exemplo chamado `calculadora`.

Funções principais:

- `servidor_calculadora(conexao)`: inicia um servidor XML-RPC local e expõe métodos `somar` e `multiplicar`.
- `demonstrar_rpc()`: registra o serviço em um diretório de nomes, descobre o endereço do serviço e chama os métodos remotamente.

Isso simula a comunicação entre processos em um ambiente distribuído, onde um cliente pode invocar funções em outro processo por rede.

### 2. Registro de nomes
A classe `RegistroDeNomes` funciona como um pequeno diretório de serviços:

- `registrar(nome, endereco)`: salva o endereço de um serviço
- `descobrir(nome)`: retorna o endereço associado

Esse mecanismo é semelhante a um DNS simples ou a um serviço de descoberta em sistemas distribuídos.

### 3. Barreira centralizada
A função `aguardar_todos(participante)` implementa uma barreira de sincronização:

- cada cliente chama a função
- quando três participantes chegam, a barreira é liberada
- se algum cliente demorar demais, o retorno é `TIMEOUT`

Isso demonstra como processos podem esperar uns aos outros antes de continuar a execução.

### 4. Relógios lógicos
A classe `Relogio` simula:

- relógio de Lamport (`lamport`)
- relógio vetorial (`vetor`)

Os métodos `evento()`, `enviar()` e `receber()` mostram como:

- um evento local incrementa o relógio
- ao receber uma mensagem, o processo integra o relógio do remetente
- essa lógica permite comparar ordem de eventos em sistemas distribuídos

A função `precede(a, b)` verifica se um vetor de eventos antecede outro.

### 5. Eleição Bully
A função `demonstrar_eleicao()` simula a eleição de um coordenador usando o algoritmo Bully:

- cada nó conhece os nós superiores a ele
- o nó inicial envia `ELECTION`
- se houver algum nó superior ativo, ele responde com `OK`
- o candidato mais alto entre os ativos torna-se coordenador

Esse algoritmo é usado em sistemas distribuídos para eleger um líder quando necessário.

### 6. Votação por maioria
A função `demonstrar_maioria()` calcula um quórum de votação:

- a maioria é `n // 2 + 1`
- se a quantidade de votos favoráveis atinge esse valor, a proposta é aprovada

Importante: a maioria isolada não é um protocolo completo de consenso, como Raft ou Paxos. Ela serve apenas para uma decisão rápida, mas não resolve todos os desafios de consistência distribuída.

## Como executar

Você pode executar o script completo com:

```bash
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py"
```

Ou selecionar apenas uma parte da demonstração:

```bash
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py" --modo rpc
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py" --modo relogios
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py" --modo eleicao
python "AVA 2 Plataformas E Sistemas De Alto Desempenho (H10325).py" --modo maioria
```

## Requisitos

- Python 3.9 ou superior
- Biblioteca padrão do Python

## Observação

Este projeto é uma simulação didática de mecanismos de sistemas distribuídos, com foco em compreender os conceitos práticos e a lógica por trás das comunicações e sincronizações entre processos.

## Conclusão

O código ilustra de forma simples e didática como diferentes mecanismos de coordenação e consistência funcionam em ambientes distribuídos, sem depender de bibliotecas externas complexas.
