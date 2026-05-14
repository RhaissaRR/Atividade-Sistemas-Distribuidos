# Atividade-Sistemas-Distribuidos
Sistema cliente-servidor para gerenciamento de estoque, vendas e parcelas de revendedoras de cosméticos.
# BeautyControl

## 1. Formação da Equipe

Repositório criado no GitHub para desenvolvimento do projeto BeautyControl.

Integrantes da equipe:
- Rhaissa Rodrigues
- Joana Martins
- Gabriela Stringasci

---

## 2. Definição do Domínio

O BeautyControl é um sistema web desenvolvido para auxiliar revendedoras de cosméticos no gerenciamento de produtos, vendas, estoque e controle de parcelas.

O sistema permite:
- Cadastro de produtos
- Controle de estoque
- Registro de vendas
- Controle de parcelas pendentes e pagas
- Consulta de clientes e produtos

A proposta surgiu para substituir controles feitos manualmente em cadernos, planilhas ou anotações dispersas, reduzindo erros de organização e melhorando o acompanhamento financeiro das vendas. Porque aparentemente a humanidade decidiu confiar dinheiro, estoque e parcelas em folhas soltas dentro de bolsas desde 1998.

### Arquitetura lógica pretendida

A arquitetura escolhida é do tipo **Cliente-Servidor**.

- Cliente:
  Interface web utilizada pelas revendedoras para acessar o sistema.

- Servidor:
  Responsável pelo processamento das informações, regras de negócio, armazenamento de dados e controle de acesso.

---

## 3. Recurso Crítico

O principal recurso crítico do sistema é o **controle de estoque dos produtos**.

Esse dado não pode ser acessado ou alterado simultaneamente por dois usuários sem controle, pois isso pode causar inconsistências na quantidade disponível dos produtos.

Exemplo:
Se duas vendas do mesmo produto forem registradas ao mesmo tempo sem controle de concorrência, o sistema pode permitir a venda de itens que não existem mais em estoque.

Por isso, o controle de atualização da quantidade dos produtos será tratado como recurso crítico do sistema, exigindo mecanismos de sincronização e consistência dos dados.
