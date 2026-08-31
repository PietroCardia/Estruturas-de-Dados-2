# Conteúdo de Revisão — Aula 03: Ponteiros, Referências e Estruturas Dinâmicas em Python

## Estrutura de Dados

**Duração:** 1h30  
**Linguagem:** Python  
**Tema:** Ponteiros de memória, referências e estruturas dinâmicas.

## 1. Objetivos de aprendizagem

Ao final da aula, o estudante deverá ser capaz de:

- compreender o conceito de endereço de memória;
- diferenciar ponteiros de referências;
- utilizar `id()` para observar a identidade de objetos;
- compreender compartilhamento de referências;
- diferenciar referência e cópia;
- compreender objetos mutáveis e imutáveis;
- criar estruturas dinâmicas utilizando referências;
- implementar nós (`Node`) e listas encadeadas;
- utilizar técnicas básicas de depuração;
- trabalhar colaborativamente.

> **Importante:** Python não possui ponteiros explícitos como C/C++. Nesta aula, o conceito de ponteiro é usado para estabelecer a base conceitual para referências e estruturas dinâmicas.

## 2. Memória e variáveis

Considere:

```python
nome = "Ana"
idade = 20
```

Uma forma didática de visualizar:

```text
nome ─────→ "Ana"
idade ────→ 20
```

Em Python, é mais adequado pensar que uma variável é um **nome associado a um objeto**.

## 3. O conceito de ponteiro

Em C:

```c
int idade = 20;
int *p = &idade;
```

Conceitualmente:

```text
idade
  │
  ▼
┌──────────┐
│    20    │
└──────────┘
     ▲
     │
     p
```

- `&` obtém o endereço;
- `*` permite trabalhar com o conteúdo apontado.

Python abstrai esse nível de manipulação.

## 4. Referências em Python

Podemos observar a identidade de um objeto com:

```python
idade = 20
print(idade)
print(id(idade))
```

`id()` retorna um identificador associado à identidade do objeto durante sua existência.

## 5. Compartilhamento de referências

```python
a = [10, 20, 30]
b = a

print(id(a))
print(id(b))
```

`a` e `b` referenciam o mesmo objeto.

```text
        ┌────────────────┐
        │ [10, 20, 30]   │
        └────────────────┘
             ▲       ▲
             │       │
             a       b
```

## 6. Referência versus cópia

### Referência

```python
a = [10, 20, 30]
b = a
b.append(40)

print(a)
print(b)
```

Resultado:

```text
[10, 20, 30, 40]
[10, 20, 30, 40]
```

### Cópia

```python
a = [10, 20, 30]
b = a.copy()
b.append(40)

print(a)
print(b)
```

Resultado:

```text
[10, 20, 30]
[10, 20, 30, 40]
```

## 7. Mutabilidade

Objetos mutáveis incluem:

```text
list
dict
set
```

Exemplo:

```python
lista = [1, 2, 3]
lista.append(4)
print(lista)
```

Objetos como `int`, `float`, `str`, `tuple` e `bool` são imutáveis.

## 8. Passagem de objetos para funções

```python
def adicionar_item(lista):
    lista.append(100)

numeros = [1, 2, 3]
adicionar_item(numeros)

print(numeros)
```

Resultado:

```text
[1, 2, 3, 100]
```

A função recebeu acesso ao mesmo objeto lista.

## 9. Estruturas dinâmicas

Estruturas dinâmicas podem crescer ou diminuir durante a execução.

Exemplos:

- listas;
- filas;
- pilhas;
- listas encadeadas;
- árvores;
- grafos.

Em Python:

```python
dados = []
dados.append(10)
dados.append(20)
dados.append(30)
print(dados)
```

## 10. Nó (`Node`)

```python
class Node:

    def __init__(self, valor):
        self.valor = valor
        self.proximo = None
```

O atributo `proximo` é uma referência para outro nó.

## 11. Criando e conectando nós

```python
node1 = Node(10)
node2 = Node(20)
node3 = Node(30)

node1.proximo = node2
node2.proximo = node3
```

Representação:

```text
10 ───→ 20 ───→ 30 ───→ None
```

## 12. Percorrendo os nós

```python
atual = node1

while atual is not None:
    print(atual.valor)
    atual = atual.proximo
```

Saída:

```text
10
20
30
```

## 13. Lista encadeada

```python
class ListaEncadeada:

    def __init__(self):
        self.inicio = None

    def adicionar(self, valor):
        novo = Node(valor)
        novo.proximo = self.inicio
        self.inicio = novo

    def exibir(self):
        atual = self.inicio

        while atual is not None:
            print(atual.valor)
            atual = atual.proximo
```

Uso:

```python
lista = ListaEncadeada()
lista.adicionar(10)
lista.adicionar(20)
lista.adicionar(30)
lista.exibir()
```

## 14. Depuração

Código com erro:

```python
atual = node1

while atual:
    print(atual.valor)
```

O programa entra em loop infinito porque `atual` nunca é atualizado.

Correção:

```python
atual = node1

while atual:
    print(atual.valor)
    atual = atual.proximo
```

Ao depurar, pergunte:

1. Qual variável está incorreta? A variável de controle de loop 
2. Qual é o valor dela? O que ela armazena 
3. Qual objeto ela referencia? Para onde o ponteiro aponta 
4. Essa referência deveria mudar? Acho que não
5. Qual condição encerra o `while`? A variável chega ao controle None 

## 15. Exercício 1 — Referências

Execute:

```python
a = [10, 20, 30]
b = a

b.append(40)

print("a:", a)
print("b:", b)
print("id(a):", id(a))
print("id(b):", id(b))
```

Responda:

1. Qual será a saída? A saída será a 10,20,30,40 nos dois primeiros e no restante vai ser um número 140123456789 mesmo sendo id diferentes.
2. `a` e `b` representam o mesmo objeto? Sim.
3. Por quê? Porque b passa a ser apenas outra referência mas objeto continua sendo o mesmo. 
4. O que aconteceria com `b = a.copy()`? Seria uma lista independente. 

## 16. Exercício 2 — Construindo uma cadeia

Crie:

```python
n1 = Node("A")
n2 = Node("B")
n3 = Node("C")
```

Conecte:

```text
A → B → C → None
```

Depois percorra a estrutura e produza:

```text
A
B
C
```

## 17. Exercício 3 — Depuração

Analise:

```python
n1 = Node(10)
n2 = Node(20)
n3 = Node(30)

n1.proximo = n2
n2.proximo = n3

atual = n1

while atual is not None:
    print(atual.valor)
```

Perguntas:

1. Qual é o problema? O laço verifica atual is not None, mas atual continua apontando para n1 indefinidamente.
2. Por que o programa não termina? Porque atual permanece igual a n1. Assim, a condição atual is not None sempre será verdadeira e 10 será impresso repetidamente.
3. Qual linha deve ser acrescentada? Dentro do while, depois do print
4. Qual será a saída depois da correção? 10 20 30

## 18. Problema real — Sistema de atendimento de uma clínica

Uma clínica recebe pacientes durante o dia. Cada paciente possui:

- nome;
- idade;
- prioridade.

Exemplo:

```text
Ana — 32 anos — Normal
Bruno — 70 anos — Prioridade
Carlos — 45 anos — Normal
```

O sistema deve permitir:

1. adicionar paciente;
2. listar pacientes;
3. atender o primeiro paciente;
4. verificar se a fila está vazia;
5. informar a quantidade de pacientes.

## 19. Modelagem

Crie:

```python
class Paciente:
    ...
```

Depois:

```python
class Node:
    ...
```

O nó deverá armazenar:

```text
paciente
próximo
```

## 20. Fila de atendimento

Crie:

```python
class FilaAtendimento:
    ...
```

A fila deverá possuir:

```text
início
fim
```

Representação:

```text
início                         fim
  ↓                             ↓
Ana  →  Bruno  →  Carlos  →  None
```

## 21. Funcionalidades obrigatórias

Implemente:

- `adicionar(paciente)`
- `atender()`
- `listar()`
- `esta_vazia()`
- `tamanho()`

## 22. Exemplo de utilização

```python
fila = FilaAtendimento()

fila.adicionar(Paciente("Ana", 32, "Normal"))
fila.adicionar(Paciente("Bruno", 70, "Prioridade"))
fila.adicionar(Paciente("Carlos", 45, "Normal"))

fila.listar()

paciente = fila.atender()
print("Atendendo:", paciente.nome)
```

## 23. Desafio — Atendimento prioritário

Amplie o sistema.

Pacientes com prioridade devem ser atendidos antes dos pacientes normais.

Exemplo:

```text
Fila inicial:

Ana    - Normal
Bruno  - Normal
Carlos - Prioridade
```

Ordem esperada:

```text
1. Carlos
2. Ana
3. Bruno
```

Antes de programar:

1. descreva a solução;
2. desenhe a estrutura;
3. escolha onde o paciente será inserido;
4. implemente;
5. teste.

## 24. Trabalho colaborativo

Forme um grupo de 2 a 4 estudantes.

### Etapa 1 — Modelar

```text
Paciente → Node → Node → Node
```

### Etapa 2 — Implementar

Criar:

```text
Paciente
Node
FilaAtendimento
```

### Etapa 3 — Testar

Teste:

- fila vazia;
- um paciente;
- vários pacientes;
- atendimento;
- remoção do último paciente;
- paciente prioritário.

### Etapa 4 — Depurar

Encontre e corrija pelo menos um erro proposital.

## 25. Exercício de revisão — Sistema de atendimento

Desenvolva individualmente uma versão funcional.

Checklist:

- [ ] Criar `Paciente`;
- [ ] Criar `Node`;
- [ ] Criar `FilaAtendimento`;
- [ ] Implementar `adicionar()`;
- [ ] Implementar `atender()`;
- [ ] Implementar `listar()`;
- [ ] Implementar `esta_vazia()`;
- [ ] Implementar `tamanho()`;
- [ ] Testar pelo menos cinco pacientes;
- [ ] Documentar um erro encontrado e sua correção.

## 26. Checklist de aprendizagem

- [ ] Entendi o conceito de endereço de memória.
- [ ] Sei diferenciar ponteiro de referência.
- [ ] Sei utilizar `id()`.
- [ ] Entendi compartilhamento de referências.
- [ ] Sei diferenciar referência e cópia.
- [ ] Entendi objetos mutáveis.
- [ ] Entendi passagem de objetos para funções.
- [ ] Consigo criar um `Node`.
- [ ] Consigo conectar nós.
- [ ] Consigo percorrer uma estrutura encadeada.
- [ ] Consigo identificar erros em uma estrutura dinâmica.
- [ ] Consigo implementar uma fila.
- [ ] Consigo explicar minha solução.

## 27. Reflexão final

### O que é uma referência em Python?

```text
Uma referência é uma forma de uma variável apontar para um objeto que está armazenado na memória.
```

### Qual a diferença entre `b = a` e `b = a.copy()`?

```text
O primeiro faz referência ao mesmo objeto. Já o segundo cria uma cópia do do objeto.
```

### Por que uma estrutura encadeada precisa de referências?

```text
Porque cada nó precisa saber onde está o próximo nó.
```

### Qual erro você encontrou durante a depuração?

```text
?
```

### Como referências ajudam a compreender estruturas dinâmicas?

```text
As referências permitem criar estruturas que podem crescer e diminuir durante a execução do programa, sem precisar definir previamente seu tamanho.
```

## 28. Síntese da aula

```text
VARIÁVEL
   ↓
REFERÊNCIA
   ↓
OBJETO
   ↓
NÓ
   ↓
ESTRUTURA DINÂMICA
   ↓
LISTA / FILA / PILHA
```

> **Uma boa estrutura de dados organiza os dados de forma que as operações necessárias sejam realizadas de maneira clara e eficiente.**

### Próxima aula

**Filas e Pilhas**

```text
Lista Encadeada
       ↓
Fila
       ↓
Pilha
       ↓
Árvore
       ↓
Grafo
```

**Boas práticas!**
