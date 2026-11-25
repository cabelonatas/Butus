# Butus

**Butus** é uma linguagem de programação em português construída em **C** e **Assembly x86_64** (`chamadas_x86_64.s`), pensada para execução direta, manipulação de dados e integração com o sistema sem depender de camadas pesadas.

Na prática, o projeto trabalha com diferentes extensões conforme o fluxo e os dados manipulados:
- **`.grr`** e **`.butus`** — arquivos de código/scripts e módulos da linguagem.
- **`.dbt`** — bases/arquivos de dados associados ao ecossistema do Butus.

---

## História e origem do nome

O nome **Butus** nasceu da inspiração no escorpião ***Buthus occitanus*** (família *Buthidae*) — uma espécie de aracnídeo conhecida pela resistência e adaptação a ambientes secos e hostis. Essa mesma ideia de resiliência, precisão e não depender de conforto excessivo guia a identidade do projeto e o ícone do escorpião.

**Autoria e desenvolvimento:** A ideia e a criação original da linguagem são do autor, com automação e apoio do **Google DeepMind** na estruturação, organização e compilação limpa.

---

## Arquitetura e o que já está no motor (`butus.c`)

Com base na implementação em C e Assembly x86_64 (`chamadas_x86_64.s`), o motor do Butus já conta com bases concretas de execução e análise:

- **Lexer e parser próprios:** tokenização de palavras-chave, identificadores, números (incluindo decimais com `.`), textos com escape (`\"`, etc.), comentários iniciados por `#` e operadores relacionais (`==`, `!=`, `<`, `>`, `<=`, `>=`).
- **Operadores lógicos em português:** suporte no lexer e na avaliação de expressões para `e` (conjunção booleana), `ou` (disjunção booleana) e `nao` (negação).
- **Tipos e estruturas:** valores numéricos, textos, listas (com indexação e concatenação), além de noções de valores nulos/verdadeiros/falsos na avaliação de condições.
- **Escopo e controle de fluxo:** variáveis e escopo local/atribuição, blocos delimitados por chaves `{ ... }`, agrupamentos com `[ ... ]` e `( ... )`, condicionais `se` / `senao` e laços de repetição.
- **Reconhecimento de diretivas e runtime:** a linha `/importar` já é identificada pelo motor (`butus_linha_parece_codigo` em `butus.c`), além de rotinas voltadas a leitura/escrita, verificação de caminhos/arquivos, execução de comandos, funções na linguagem, escuta de porta e montagem de saída HTML quando em modo correspondente.

---

## Referência rápida de sintaxe e convenções

### Palavras-chave, diretivas e construções principais
- `/importar` — diretiva reconhecida pelo motor para importação de módulos `.grr` e bibliotecas (carregamento de módulos externos em evolução no motor).
- `definir` — cria ou atribui valores a variáveis (ex.: `definir total = 0`).
- `exibir` / `escrever` — exibe saídas/mensagens ou grava/registra informações.
- `ler` — captura entrada ou lê dados.
- `se` / `senao` — desvio condicional conforme a expressão avaliada.
- `enquanto` / `para` — estruturas de repetição.
- `funcao` / `retornar` / `interromper` — rotinas, devolução de valor e interrupção de fluxo.
- `executar` / `verificar` — disparo de ações/comandos e checagens/validações.

### Convenções de escrita
- **Sem ponto e vírgula (`;`)** no final das linhas.
- **Ponto (`.`)** para números decimais (ex.: `10.5`).
- **Vírgula (`,`)** para separar itens e argumentos.
- **Cerquilha (`#`)** para comentários de linha.
- **Delimitadores:** `{ ... }` para blocos, `[ ... ]` para expressões/condições e `( ... )` para parâmetros/argumentos.
- **Lógica booleana:** use `e`, `ou` e `nao` nas condições.

---

## Módulos e bibliotecas (`.grr`)

A organização em módulos `.grr` e bibliotecas separa responsabilidades e facilita o reuso de código no projeto. A diretiva `/importar` já consta na detecção de código do `butus.c`, enquanto a execução completa do carregamento de módulos/bibliotecas avança no motor:

```butus
# Exemplo de declaração com /importar para módulos .grr e bibliotecas
/importar "modulos/utilidades.grr"
/importar "libs/sistema.grr"
