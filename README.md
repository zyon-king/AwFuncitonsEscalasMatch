# AwFuncitonsEscalasMatch
# Sistema de Validação de Token

Uma aplicação web para controle de acesso através de validação de tokens, utilizando Appwrite Functions para autenticação segura.

## 📋 Funcionalidades

- **Interface de Login**: Formulário elegante para inserção do token de acesso
- **Validação Segura**: Token secreto armazenado como variável de ambiente no backend
- **Feedback Visual**: Mensagens de status em tempo real com cores indicativas
- **Design Responsivo**: Interface adaptável para diferentes dispositivos
- **Segurança**: Comparação de tokens no servidor, não no frontend

## 🚀 Tecnologias Utilizadas

### Frontend
- HTML5
- CSS3 (Design moderno com gradientes e transições)
- JavaScript ES6+ (Async/Await, Modules)
- Appwrite SDK v20.0.0

### Backend
- Appwrite Functions (Node.js Runtime)
- Variáveis de ambiente para segurança

## 🛠️ Configuração

### 1. Configuração do Appwrite

#### Projeto Appwrite
- Endpoint: `https://nyc.cloud.appwrite.io/v1`
- Project ID: `686a67d5003a1b4b1bf9`

#### Configuração de CORS
Adicione as seguintes plataformas web no console do Appwrite:
- `*.googleusercontent.com` (para W3Schools e plataformas similares)
- `localhost` (para desenvolvimento local)
- Seu domínio de produção

### 2. Função de Validação

#### Criação da Função
1. Acesse o console do Appwrite
2. Vá para "Functions" > "Create Function"
3. Configure:
   - **Name**: `validaToken`
   - **Runtime**: Node.js
   - **Trigger**: HTTP

#### Código da Função (index.js)
```javascript
module.exports = async ({ req, res, log, error }) => {
  // Pega o token enviado pelo site
  const tokenFornecido = req.body.token;
  
  // Pega o token secreto da variável de ambiente
  const tokenSecreto = process.env.TOKEN_SECRETO;
  
  // Compara os dois tokens
  if (tokenFornecido === tokenSecreto) {
    return res.json({ success: true, message: 'Acesso liberado!' });
  } else {
    return res.json({ success: false, message: 'Token inválido.' }, 401);
  }
};
```

#### Configuração de Variáveis de Ambiente
1. Na função criada, vá para "Settings" > "Variables"
2. Adicione:
   - **Key**: `TOKEN_SECRETO`
   - **Value**: Seu token secreto (ex: `meuTokenSecreto123`)

#### Deploy da Função
1. Faça upload dos arquivos ou use Git
2. Aguarde o build e deploy
3. Anote o Function ID (ex: `68c5be1b00315ff07f89`)

## 📁 Estrutura do Projeto

```
/
├── index.html              # Página principal com interface de login
├── README.md              # Este arquivo
└── appwrite-function/     # Função do Appwrite
    ├── index.js          # Lógica de validação do token
    └── package.json      # Dependências (se necessário)
```

## 🎨 Personalização Visual

### Cores do Tema
- **Background**: `#2c3e50` (Azul escuro)
- **Container**: `#34495e` (Azul médio)
- **Botão**: `#1abc9c` (Verde água)
- **Texto**: `#ecf0f1` (Branco suave)
- **Sucesso**: `#2ecc71` (Verde)
- **Erro**: `#e74c3c` (Vermelho)
- **Aguardando**: `#f1c40f` (Amarelo)

### Estados Visuais
- **Normal**: Texto branco em fundo escuro
- **Verificando**: Texto amarelo "Verificando token..."
- **Sucesso**: Texto verde "Token correto! Acesso liberado."
- **Erro**: Texto vermelho "Token inválido. Tente novamente."

## 🔧 Como Usar

### 1. Configuração Inicial
1. Configure seu projeto Appwrite
2. Crie e deploy a função de validação
3. Configure a variável de ambiente `TOKEN_SECRETO`
4. Atualize o Function ID no código HTML

### 2. Execução
1. Abra o arquivo HTML no navegador
2. Digite o token no campo de entrada
3. Clique em "Acessar"
4. Aguarde a validação

### 3. Integração
Após validação bem-sucedida, você pode:
- Redirecionar para página restrita: `window.location.href = "pagina-restrita.html"`
- Mostrar conteúdo oculto: `document.getElementById('conteudo').style.display = 'block'`
- Armazenar estado de autenticação: `sessionStorage.setItem('authenticated', 'true')`

## 🐛 Solução de Problemas

### Erro "Cannot find module 'appwrite'"
**Solução**: Remova a linha `const { Appwrite } = require('appwrite');` do `index.js` da função, pois não é necessária para validação simples.

### Erro "is not valid JSON"
**Solução**: Use `response.responseBody` em vez de `response.body`:
```javascript
const result = JSON.parse(response.responseBody || response.body || '{}');
```

### Erro de CORS
**Solução**: Adicione o domínio/wildcard correto nas plataformas web do Appwrite:
- Para W3Schools: `*.googleusercontent.com`
- Para desenvolvimento: `localhost`
- Para produção: seu domínio

### Token sempre inválido
**Verificações**:
1. Variável `TOKEN_SECRETO` está configurada na função
2. Função está deployada corretamente
3. Function ID está correto no HTML
4. Token digitado corresponde ao configurado

## 🔐 Considerações de Segurança

### Boas Práticas Implementadas
- Token secreto armazenado no servidor (variável de ambiente)
- Comparação de tokens no backend
- Input type="password" para ocultar token
- Validação server-side

### Recomendações Adicionais
- Use tokens complexos e únicos
- Implemente rate limiting
- Adicione logs de tentativas de acesso
- Configure HTTPS em produção
- Considere tokens com expiração

## 📊 Logs e Monitoramento

### Verificação de Execuções
1. Acesse "Functions" no console Appwrite
2. Selecione sua função `validaToken`
3. Vá para "Executions"
4. Verifique logs de sucesso/erro

### Debug no Frontend
Adicione console.logs para debugging:
```javascript
console.log('Response completa:', response);
console.log('Response.responseBody:', response.responseBody);
```

## 🚀 Deploy

### Opções de Hospedagem
1. **GitHub Pages** (gratuito)
2. **Netlify** (gratuito)
3. **Vercel** (gratuito)
4. **Servidor próprio**

### Configuração CORS para Produção
Lembre-se de adicionar seu domínio de produção nas plataformas web do Appwrite.

## 📞 Suporte

Para problemas ou dúvidas:
1. Verifique os logs da função no console Appwrite
2. Confirme configurações de CORS
3. Teste a função diretamente no console Appwrite
4. Verifique se a variável de ambiente está configurada

---

**Desenvolvido com Appwrite Functions e JavaScript ES6+**
