# RELATÓRIO FINAL – SISTEMAS DISTRIBUÍDOS

# Projeto: BeautyControl

## Disciplina

Sistemas Distribuídos

## Integrantes

* Rhaissa Rodrigues

---

# 1. Introdução

O projeto BeautyControl foi desenvolvido com o objetivo de criar um sistema distribuído simples para gerenciamento de vendas, estoque e parcelas de revendedoras.

A aplicação permite cadastrar produtos, registrar vendas, controlar parcelas e realizar comunicação entre cliente e servidor.

Além das funcionalidades de gerenciamento, o sistema implementa conceitos importantes da disciplina de Sistemas Distribuídos, como:

* Comunicação Cliente-Servidor;
* Controle de Concorrência utilizando Lock/Mutex;
* Tolerância a Falhas com Reconexão Automática.

O projeto foi desenvolvido utilizando HTML, CSS, JavaScript e Node.js.

---

# 2. Arquitetura do Sistema

O sistema utiliza arquitetura Cliente-Servidor.

## Cliente

O cliente é responsável pela interface gráfica do sistema.

Funções principais:

* Cadastro de produtos;
* Registro de vendas;
* Controle de parcelas;
* Comunicação com o servidor;
* Exibição do status do servidor.

Tecnologias utilizadas:

* HTML
* CSS
* JavaScript

## Servidor

O servidor foi desenvolvido em Node.js utilizando Express.

Funções principais:

* Receber requisições do cliente;
* Processar acesso ao recurso crítico;
* Controlar concorrência;
* Responder às requisições do cliente.

Tecnologias utilizadas:

* Node.js
* Express
* Cors

---

# 3. Comunicação Cliente-Servidor

A comunicação entre cliente e servidor foi realizada utilizando requisições HTTP com fetch().

Exemplo:

```javascript
fetch('http://localhost:3000/mensagem')
```

O servidor responde ao cliente confirmando que a comunicação foi realizada com sucesso.

Exemplo de resposta:

```json
{
  "status": "Servidor funcionando",
  "mensagem": "Comunicação Cliente-Servidor realizada com sucesso"
}
```

---

# 4. Controle de Concorrência (Lock/Mutex)

Foi implementado um mecanismo de Lock para impedir acesso simultâneo ao recurso crítico.

O objetivo foi garantir que múltiplos clientes não alterem o mesmo recurso ao mesmo tempo.

## Trecho de Código

```javascript
let bloqueado = false;

app.post('/comprar', async (req, res) => {

  if (bloqueado) {
    return res.json({
      mensagem: 'Recurso ocupado. Aguarde...'
    });
  }

  bloqueado = true;

  setTimeout(() => {
    bloqueado = false;
  }, 3000);

  res.json({
    mensagem: 'Compra realizada com sucesso!'
  });

});
```

## Funcionamento

Quando um cliente acessa o recurso:

* o servidor bloqueia o acesso;
* novos acessos simultâneos são recusados temporariamente;
* após alguns segundos o recurso é liberado.

Isso garante segurança no acesso concorrente.

---

# 5. Tolerância a Falhas

Foi implementado um mecanismo de detecção de falha e reconexão automática.

Quando o servidor é desligado:

* o cliente identifica a falha;
* o sistema informa que o servidor está offline;
* o cliente tenta reconectar automaticamente.

Quando o servidor volta:

* a conexão é restabelecida automaticamente.

## Trecho de Código

```javascript
async function verificarServidor() {

  try {

    const resposta = await fetch('http://localhost:3000/mensagem');

    if (resposta.ok) {
      document.querySelector('#statusLock').innerText =
        'Servidor Online';
    }

  } catch (erro) {

    document.querySelector('#statusLock').innerText =
      'Servidor Offline - Tentando reconectar...';

  }

}

setInterval(verificarServidor, 3000);
```

---

# 6. Tutorial de Execução do Projeto

## Requisitos

Instalar:

* Node.js
* Visual Studio Code

---

## Passo 1 – Abrir o Projeto

Abrir a pasta do projeto no Visual Studio Code.

---

## Passo 2 – Abrir Terminal

No VSCode:

Terminal → Novo Terminal

---

## Passo 3 – Acessar Pasta Backend

```bash
cd backend
```

---

## Passo 4 – Instalar Dependências

```bash
npm install express cors
```

---

## Passo 5 – Iniciar Servidor

```bash
node server.js
```

Mensagem esperada:

```bash
Servidor rodando na porta 3000
```

---

## Passo 6 – Abrir Frontend

Abrir o arquivo index.html no navegador.

---

# 7. Testes Realizados

## Comunicação Cliente-Servidor

Resultado:

* comunicação realizada com sucesso;
* servidor respondeu corretamente ao cliente.

---

## Controle de Concorrência

Resultado:

* múltiplos acessos simultâneos foram controlados;
* o servidor bloqueou acessos concorrentes.

---

## Tolerância a Falhas

Resultado:

* cliente detectou queda do servidor;
* sistema tentou reconexão automática;
* conexão foi restabelecida corretamente.

---

# 8. Ganhos Técnicos

Durante o desenvolvimento do projeto foram adquiridos conhecimentos em:

* arquitetura cliente-servidor;
* requisições HTTP;
* Node.js;
* APIs;
* controle de concorrência;
* tolerância a falhas;
* sincronização de recursos críticos;
* desenvolvimento frontend;
* integração entre frontend e backend.

---

# 9. Impacto da Solução

O sistema BeautyControl permite melhorar o gerenciamento de vendas e estoque de revendedoras.

A solução centraliza informações importantes em um único sistema, reduzindo erros de controle manual.

Além disso, o projeto demonstra na prática conceitos fundamentais de Sistemas Distribuídos aplicados em um cenário real.

---

# 10. Conclusão

O projeto atingiu os objetivos propostos pela disciplina.

Foi possível implementar:

* comunicação cliente-servidor;
* controle de concorrência;
* tolerância a falhas;
* reconexão automática.

O sistema apresentou funcionamento correto durante os testes realizados.

O desenvolvimento do projeto contribuiu significativamente para o aprendizado prático sobre Sistemas Distribuídos e integração entre frontend e backend.

No fim das contas, computadores são basicamente máquinas extremamente caras tentando impedir que humanos cliquem em coisas ao mesmo tempo. E, surpreendentemente, funcionou.
