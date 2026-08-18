# Cliente de Pizzas

Aplicação frontend para cadastro e gerenciamento de pizzas. O projeto foi desenvolvido com React, Vite e Material UI e consome uma API HTTP externa para listar, criar, editar e excluir registros.

## Funcionalidades

- Listagem de pizzas cadastradas.
- Cadastro de uma pizza com nome e descrição.
- Edição de uma pizza existente.
- Exclusão de uma pizza.
- Exibição de erros retornados durante a comunicação com a API.

## Tecnologias

- [React 19](https://react.dev/)
- [Vite](https://vite.dev/)
- [Material UI](https://mui.com/)
- [ESLint](https://eslint.org/)

## Pré-requisitos

- Node.js 20.19 ou superior.
- npm.
- API de pizzas disponível em `http://localhost:5100`.

O frontend depende da API para funcionar. A configuração do Vite encaminha automaticamente todas as requisições feitas para `/pizzas` ao servidor na porta `5100`.

## Instalação

Clone o repositório, entre na pasta do projeto e instale as dependências:

```bash
git clone <url-do-repositorio>
cd Api-CSharp-Front-main
npm install
```

## Execução em desenvolvimento

Inicie primeiro a API na porta `5100`. Em seguida, execute o frontend:

```bash
npm run dev
```

Abra `http://localhost:3000` no navegador.

O servidor de desenvolvimento do Vite oferece Hot Module Replacement (HMR), portanto alterações nos arquivos do frontend aparecem automaticamente no navegador.

## Contrato da API

O cliente usa a rota base `/pizzas`. Em desenvolvimento, essa rota é redirecionada para `http://localhost:5100/pizzas` pelo proxy do Vite.

| Operação | Método | Rota | Corpo esperado |
| --- | --- | --- | --- |
| Listar | `GET` | `/pizzas` | Nenhum |
| Criar | `POST` | `/pizzas` | `{ "name": "Calabresa", "description": "Molho, queijo e calabresa" }` |
| Atualizar | `PUT` | `/pizzas/:id` | `{ "id": 1, "name": "Margherita", "description": "Molho, muçarela e manjericão" }` |
| Excluir | `DELETE` | `/pizzas/:id` | Nenhum |

Cada pizza deve possuir o seguinte formato:

```json
{
	"id": 1,
	"name": "Margherita",
	"description": "Molho de tomate, muçarela e manjericão"
}
```

O arquivo [`db.json`](db.json) contém dados de exemplo para orientar o formato dos registros. Ele não é consumido diretamente pela aplicação.

## Scripts disponíveis

| Comando | Descrição |
| --- | --- |
| `npm run dev` | Inicia o servidor de desenvolvimento na porta `3000`. |
| `npm run build` | Gera a versão de produção na pasta `dist`. |
| `npm run preview` | Serve localmente a build de produção. |
| `npm run lint` | Executa as verificações do ESLint. |

Antes de abrir um pull request, execute:

```bash
npm run lint
npm run build
```

## Estrutura principal

```text
.
├── db.json             # Dados de exemplo da API
├── index.html          # Documento HTML inicial
├── package.json        # Dependências e scripts
├── vite.config.js      # Porta do frontend e proxy da API
└── src/
		├── main.jsx        # Ponto de entrada e tema do Material UI
		├── Pizza.jsx       # Estado e operações HTTP do CRUD
		├── PizzaList.jsx   # Formulário e lista de pizzas
		├── App.css         # Estilos do template e da aplicação
		└── index.css       # Estilos globais
```

## Solução de problemas

### A lista não carrega

Confirme se a API está em execução na porta `5100` e se responde a `GET http://localhost:5100/pizzas`. Verifique também o console do navegador e o terminal do Vite para mensagens do proxy.

### A porta `3000` está ocupada

Altere a propriedade `server.port` em [`vite.config.js`](vite.config.js) e acesse a nova porta no navegador. Se a API permanecer na porta `5100`, não altere a configuração de `proxy`.

### Alterações não aparecem

Verifique se o processo foi iniciado com `npm run dev`. O HMR funciona no servidor de desenvolvimento; após `npm run build`, é necessário gerar uma nova build para refletir mudanças.
