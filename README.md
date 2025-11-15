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
* Digite um comando (help para opções): add
* ID do item: 5
* Nome: Exemplo 01
* Quantidade: 15
* Categoria: Exemplos 
* Item adicionado com sucesso.
*
* `remove`: Inicia o prompt para remover (dar baixa) em uma quantidade de um item existente (por ID).
* Digite um comando (help para opções): remove
* ID do item: 5
* Quantidade a remover: 10
* Remoção aplicada.
*
* `update`: Permite atualizar nome, quantidade e/ou categoria de um item (deixe o campo em branco para manter o valor atual).
* Digite um comando (help para opções): update
* ID do item: 5
* Novo nome (Enter para manter): Exemplo Alterado
* Nova quantidade (Enter para manter): 20
* Nova categoria (Enter para manter): 
* Item atualizado.
*
* `query`: Consulta e exibe os detalhes de um único item (por ID).
* Digite um comando (help para opções): query
* ID do item: 5
* Item encontrado: Item {itemID = "5", nome = "Exemplo Alterado", quantidade = 20, categoria = "Exemplos "}
* 
* `list`: Lista todos os itens atualmente em memória no inventário.
* Digite um comando (help para opções): list
*
* --- Inventário Atual ---
* - 1: Teste 01 | qtd=20 | categoria=Sujeito de Teste
* - 2: Teste 02 | qtd=40 | categoria=Sujeito de Teste
* - 3: Teste 03 | qtd=80 | categoria=Sujeito de Teste
* - 4: Teste 04 | qtd=10 | categoria=Sujeito de Teste
* - 5: Exemplo Alterado | qtd=20 | categoria=Exemplos 
* -----------------------
* 
* `report`: Gera relatórios de auditoria com base no `Auditoria.log` (histórico por item, logs de erro, item mais movimentado).
* Digite um comando (help para opções): report
* 
* ===== Relatório de Auditoria =====
* Total de entradas registradas: 10
* Item para histórico detalhado (Enter para pular): (Aqui você escreve o código do Produto que deseja ver as mudanças realizadas ou ENTER para ver os erros)
* 
* Falhas registradas: 2
*   2025-11-15 00:04:53.110086095 UTC | Remove | Falha: Estoque insuficiente | item=4 :: Tentativa de remover -> Estoque insuficiente
 *  2025-11-15 00:17:48.457991125 UTC | Add | Falha: Item já existe no inventário (ID duplicado) | item=1 :: Tentativa de adicionar -> Item já existe no inventário (ID * duplicado)
* 
* Item mais movimentado: 5 (3 operações)
* ==================================
* 
* `help`: Exibe este menu de comandos.
* Digite um comando (help para opções): help
* 
* Comandos disponíveis:
*   add       - adicionar novo item
*   remove    - remover unidades de um item
*   update    - atualizar campos de um item
*   query     - consultar item
*   list      - listar inventário completo
*   report    - gerar relatório baseado nos logs
*   help      - mostrar este menu
*   exit      - sair do sistema
* 
* `exit`: Salva o estado atual no `Inventario.dat` e encerra o programa.
* Digite um comando (help para opções): exit
* Estado salvo. Encerrando...

---

## 5. Dados Mínimos de Teste (Req 4.1)

Para validar os relatórios, o sistema foi populado com 10 itens distintos.

**Execução (Terminal):**
