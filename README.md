# Sistema de Inventário Haskell

Este projeto é um sistema de gerenciamento de inventário interativo via terminal, desenvolvido em Haskell. O objetivo é aplicar conceitos de programação funcional, separando rigorosamente a lógica pura (manipulação de estado) das operações impuras (I/O), e garantir a persistência dos dados e um log de auditoria robusto.

---

## 1. Informações da Equipe (Req 5)

* **Instituição:** [Substitua pelo Nome da Instituição]
* **Disciplina:** [Substitua pelo Nome da Disciplina]
* **Professor:** [Substitua pelo Nome do Professor]

### Alunos
* **Nome Aluno 1** (GitHub: `usuario1`)
* **Nome Aluno 2** (GitHub: `usuario2`)
* **Nome Aluno 3** (GitHub: `usuario3`)

---

## 2. Link de Execução (Req 1, 5)

O projeto pode ser executado, testado e compilado sem modificações diretamente no GDB Online através do seguinte link:

**[Link para o GDB Online com o projeto pronto para rodar]**
*(Substitua este texto pelo link "Share" do GDB Online)*

---

## 3. Como Compilar e Executar (Req 5)

O projeto consiste em um único arquivo `Main.hs` e não requer bibliotecas externas além das que acompanham o GHC (como `Data.Map` e `Data.Time`).

### Executando no GDB Online
1.  Abra o link fornecido na Seção 2.
2.  Clique no botão **"Run"** (Verde) no topo da tela.
3.  O código será compilado e o programa iniciará no terminal inferior.

### Executando Localmente (via GHCi)
1.  Certifique-se de ter o [GHC (Glasgow Haskell Compiler)](https://www.haskell.org/ghcup/) instalado.
2.  Navegue até o diretório do projeto.
3.  Carregue o módulo no GHCi:
    ```bash
    $ ghci Main.hs
    ```
4.  Execute a função principal:
    ```haskell
    Prelude> :main
    ```

### Arquivos Gerados
O programa utiliza dois arquivos para persistência (Req 2.2, 3):
* `Inventario.dat`: Armazena o estado atual do inventário. É **sobrescrito** a cada operação de sucesso.
* `Auditoria.log`: Armazena **todas** as tentativas de operação (sucesso ou falha) em modo "append-only".

---

## 4. Comandos do Sistema

O programa funciona com os seguintes comandos interativos:

* `add`: Inicia o prompt para adicionar um novo item (ID, Nome, Quantidade, Categoria).
* `remove`: Inicia o prompt para remover (dar baixa) em uma quantidade de um item existente (por ID).
* `update`: Permite atualizar nome, quantidade e/ou categoria de um item (deixe o campo em branco para manter o valor atual).
* `query`: Consulta e exibe os detalhes de um único item (por ID).
* `list`: Lista todos os itens atualmente em memória no inventário.
* `report`: Gera relatórios de auditoria com base no `Auditoria.log` (histórico por item, logs de erro, item mais movimentado).
* `help`: Exibe este menu de comandos.
* `exit`: Salva o estado atual no `Inventario.dat` e encerra o programa.

---

## 5. Dados Mínimos de Teste (Req 4.1)

# Testes Manuais:

## Cenário 1: Persistência de Estado (Sucesso)

[1 of 2] Compiling Main             ( main.hs, main.o )
[2 of 2] Linking a.out
Sistema de Inventário Haskell
=================================================
Itens carregados: 0
Nenhum log de auditoria anterior encontrado.

Comandos disponíveis:
  add       - adicionar novo item
  remove    - remover unidades de um item
  update    - atualizar campos de um item
  query     - consultar item
  list      - listar inventário completo
  report    - gerar relatório baseado nos logs
  help      - mostrar este menu
  exit      - sair do sistema

Digite um comando (help para opções): add
ID do item: 1
Nome: Teste 01
Quantidade: 20
Categoria: Sujeito de Teste
Item adicionado com sucesso.

Digite um comando (help para opções): add
ID do item: 2
Nome: Teste 02
Quantidade: 40
Categoria: Sujeito de Teste
Item adicionado com sucesso.

Digite um comando (help para opções): add
ID do item: 3
Nome: Teste 03
Quantidade: 80
Categoria: Sujeito de Teste
Item adicionado com sucesso.

### Após finalizar o programa os arquivos (Auditoria.log e Inventario.dat) foram criados com as respectivas ações.

Auditoria.log: 
LogEntry {timestamp = 2025-11-14 23:58:39.485468905 UTC, acao = Add, detalhes = "item=1 :: Adicionado: Teste 01", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:58:54.253775977 UTC, acao = Add, detalhes = "item=2 :: Adicionado: Teste 02", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:59:14.617617937 UTC, acao = Add, detalhes = "item=3 :: Adicionado: Teste 03", status = Sucesso}

Inventario.dat:
fromList [("1",Item {itemID = "1", nome = "Teste 01", quantidade = 20, categoria = "Sujeito de Teste"}),("2",Item {itemID = "2", nome = "Teste 02", quantidade = 40, categoria = "Sujeito de Teste"}),("3",Item {itemID = "3", nome = "Teste 03", quantidade = 80, categoria = "Sujeito de Teste"})]

### Reiniciando o programa:
[1 of 2] Compiling Main             ( main.hs, main.o )
[2 of 2] Linking a.out
Sistema de Inventário Haskell (Projeto de Estudo)
=================================================
Itens carregados: 3
Últimos 5 registros (Auditoria.log):
LogEntry {timestamp = 2025-11-14 23:58:39.485468905 UTC, acao = Add, detalhes = "item=1 :: Adicionado: Teste 01", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:58:54.253775977 UTC, acao = Add, detalhes = "item=2 :: Adicionado: Teste 02", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:59:14.617617937 UTC, acao = Add, detalhes = "item=3 :: Adicionado: Teste 03", status = Sucesso}

Comandos disponíveis:
  add       - adicionar novo item
  remove    - remover unidades de um item
  update    - atualizar campos de um item
  query     - consultar item
  list      - listar inventário completo
  report    - gerar relatório baseado nos logs
  help      - mostrar este menu
  exit      - sair do sistema

Digite um comando (help para opções): list

--- Inventário Atual ---
- 1: Teste 01 | qtd=20 | categoria=Sujeito de Teste
- 2: Teste 02 | qtd=40 | categoria=Sujeito de Teste
- 3: Teste 03 | qtd=80 | categoria=Sujeito de Teste
------------------------

## Cenário 2: Erro de Lógica (Estoque Insuficiente)

Comandos disponíveis:
  add       - adicionar novo item
  remove    - remover unidades de um item
  update    - atualizar campos de um item
  query     - consultar item
  list      - listar inventário completo
  report    - gerar relatório baseado nos logs
  help      - mostrar este menu
  exit      - sair do sistema

Digite um comando (help para opções): add
ID do item: 4
Nome: Teste 04 
Quantidade: 10
Categoria: Sujeito de Teste
Item adicionado com sucesso.

Digite um comando (help para opções): remove
ID do item: 4
Quantidade a remover: 15
Erro: Estoque insuficiente

### Verificando os arquivos Auditoria.log e Inventario.dat

Auditoria.log:

LogEntry {timestamp = 2025-11-14 23:58:39.485468905 UTC, acao = Add, detalhes = "item=1 :: Adicionado: Teste 01", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:58:54.253775977 UTC, acao = Add, detalhes = "item=2 :: Adicionado: Teste 02", status = Sucesso}
LogEntry {timestamp = 2025-11-14 23:59:14.617617937 UTC, acao = Add, detalhes = "item=3 :: Adicionado: Teste 03", status = Sucesso}
LogEntry {timestamp = 2025-11-15 00:04:40.5459967 UTC, acao = Add, detalhes = "item=4 :: Adicionado: Teste 04", status = Sucesso}
LogEntry {timestamp = 2025-11-15 00:04:53.110086095 UTC, acao = Remove, detalhes = "item=4 :: Tentativa de remover -> Estoque insuficiente", status = Falha "Estoque insuficiente"} 

Inventario.dat:

fromList [("1",Item {itemID = "1", nome = "Teste 01", quantidade = 20, categoria = "Sujeito de Teste"}),("2",Item {itemID = "2", nome = "Teste 02", quantidade = 40, categoria = "Sujeito de Teste"}),("3",Item {itemID = "3", nome = "Teste 03", quantidade = 80, categoria = "Sujeito de Teste"}),("4",Item {itemID = "4", nome = "Teste 04", quantidade = 10, categoria = "Sujeito de Teste"})]

### Como foi possível ver o erro apareceu no log da Auditoria e a quantidade de Itens no inventario.dat não diminuiu por conta do erro.

## Cenário 3: Geração de Relatório de Erros

Comandos disponíveis:
  add       - adicionar novo item
  remove    - remover unidades de um item
  update    - atualizar campos de um item
  query     - consultar item
  list      - listar inventário completo
  report    - gerar relatório baseado nos logs
  help      - mostrar este menu
  exit      - sair do sistema

Digite um comando (help para opções): report

===== Relatório de Auditoria =====
Total de entradas registradas: 5
Item para histórico detalhado (Enter para pular): 

Falhas registradas: 1
  2025-11-15 00:04:53.110086095 UTC | Remove | Falha: Estoque insuficiente | item=4 :: Tentativa de remover -> Estoque insuficiente

Item mais movimentado: 4 (2 operações)
==================================

### Como foi possível ver o relatório gerado após a utilização do comando "report"  nos mostra o ERRO cometido no Cenário 2 (a tentativa de remover
estoque insuficiente).

**Execução (Terminal):**
