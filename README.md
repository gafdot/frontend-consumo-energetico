## Documentação do Projeto: Monitoramento de Sensores com Autenticação JWT

### 1. Visão Geral
Este projeto é uma aplicação web para monitoramento de dados de sensores, permitindo que usuários registrem contas, façam login, e visualizem gráficos de dados de sensores. A comunicação com o backend é feita através de requisições HTTP protegidas com autenticação via token JWT. A aplicação inclui funcionalidades como gráficos dinâmicos de temperatura e umidade, atualização automática dos dados, e controle de estado dos serviços.

### 2. Arquitetura do Projeto
A arquitetura do projeto é baseada em componentes React e utiliza o `react-router-dom` para navegação. A autenticação de usuários é feita por meio de um token JWT armazenado no `localStorage`, que permite acesso às páginas protegidas da aplicação. A aplicação consiste dos seguintes arquivos principais:

- `main.jsx`: Ponto de entrada da aplicação que renderiza o componente `App`.
- `App.jsx`: Componente principal que define as rotas da aplicação e gerencia a autenticação.
- `SensorDataChart.jsx`: Componente para exibir gráficos de dados de sensores de temperatura e umidade.
- `HomePage.jsx`: Página inicial com opções para acessar os dados dos sensores e fazer logout.
- `RegisterForm.jsx` e `LoginForm.jsx`: Formulários de registro e login para usuários.

### 3. Estrutura de Pastas

```plaintext
/src
├── App.jsx                # Componente principal e rotas da aplicação
├── BotaoLimparDados.jsx   # Botão para limpar dados do sensor (não incluído acima)
├── BotaoPausarReiniciarServico.jsx # Botão para pausar/reiniciar serviço de dados (não incluído acima)
├── HomePage.jsx           # Página inicial após login
├── LoginForm.jsx          # Formulário de login
├── RegisterForm.jsx       # Formulário de registro
├── SensorDataChart.jsx    # Componente para exibição de dados dos sensores
└── main.jsx               # Ponto de entrada da aplicação
```

### 4. Pré-requisitos
- Node.js (versão 14 ou superior)
- Backend para autenticação JWT e manipulação de dados (endereço padrão: `http://localhost:3000`)

### 5. Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/gafdot/frontend-IoT-reactjs-vite
   ```
2. Acesse o diretório do projeto:
   ```bash
   cd frontend-IoT-reactjs-vite
   ```
3. Instale as dependências:
   ```bash
   npm install
   ```
4. Instale as dependências para o Chart.js e React Router:
   ```bash
   npm install chart.js react-chartjs-2 react-router-dom react-toastify flowbite-react
   ```

### 6. Configuração

- No backend, defina rotas para autenticação de usuários (`/login`, `/register`) e para acessar ou registrar dados dos sensores (`/dados-sensores`).
- No `SensorDataChart.jsx`, ajuste a URL base do backend conforme necessário:
  ```javascript
  const response = await fetch('http://localhost:3000/dados-sensores', { ... });
  ```

### 7. Uso

#### Executando o Projeto
1. Para iniciar a aplicação em modo de desenvolvimento:
   ```bash
   npm start
   ```
2. Abra o navegador e acesse `http://localhost:3000`.

#### Fluxo de Navegação
- Ao acessar a aplicação, o usuário é redirecionado para a tela de login, caso não esteja autenticado.
- Após o login, o usuário é direcionado para a `HomePage`, onde pode acessar os dados dos sensores.
- Na página de dados dos sensores, gráficos de temperatura e umidade são atualizados automaticamente a cada 30 segundos. É possível pausar/retomar o serviço e limpar os dados exibidos.

### 8. Detalhamento dos Arquivos

#### `main.jsx`
Arquivo de entrada que importa e renderiza o componente `App` dentro do elemento `root`.

#### `App.jsx`
Define as rotas principais da aplicação. Utiliza `isAuthenticated` para verificar a presença do token JWT e controlar o acesso às rotas. Rotas protegidas (`/` e `/sensores`) redirecionam o usuário para o login, caso o token não esteja presente.

#### `SensorDataChart.jsx`
Componente responsável pela exibição dos gráficos. Periodicamente envia e recebe dados simulados de temperatura e umidade, atualizando os gráficos. Implementa:
- **Chart.js** para visualização dos dados.
- **Atualização automática**: um `useEffect` configura um intervalo para atualização a cada 30 segundos.
- **Autenticação com Token**: Requisições incluem o token JWT armazenado em `localStorage`.

#### `HomePage.jsx`
Página inicial acessível após login. Contém botões para navegação:
- **Visualizar Dados dos Sensores**: Redireciona para `/sensores`.
- **Logout**: Remove o token JWT e redireciona para `/login`.

#### `RegisterForm.jsx`
Formulário de cadastro de usuário. Envia dados para o backend, exibe mensagens de sucesso ou erro com o `react-toastify`.

#### `LoginForm.jsx`
Formulário de login de usuário. Após a autenticação bem-sucedida, armazena o token JWT em `localStorage` e redireciona para a página inicial. Em caso de erro, exibe notificações usando `react-toastify`.

### 9. Testando a Aplicação
1. **Registro de Usuário**: Teste criando um novo usuário em `/register`.
2. **Login de Usuário**: Teste o fluxo de login com as credenciais recém-criadas.
3. **Visualização de Dados dos Sensores**: Acesse `/sensores` e verifique a exibição dos gráficos e a atualização automática dos dados.
4. **Logout**: Confirme o logout para garantir que o token é removido e o acesso é restrito.

### 10. Considerações Finais
Este projeto fornece uma base sólida para uma aplicação de monitoramento de dados de sensores com autenticação. O uso do token JWT garante segurança nas operações de leitura e envio de dados, enquanto o `Chart.js` permite visualizações dinâmicas e interativas. Essa estrutura é facilmente expansível para incluir novos tipos de dados ou funcionalidades.