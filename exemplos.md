// =========  
// index.js  
// =========  

// exemplo de sintaxe de uma Aw Fx

```
module.exports = async ({ req, res, log, error }) => {
  // 1. Pega o token enviado pelo site
  const tokenFornecido = req.body.token;
  // 2. Pega o token secreto da variável de ambiente
  const tokenSecreto = process.env.TOKEN_SECRETO;
  // 3. Compara os dois tokens
  if (tokenFornecido === tokenSecreto) {
    // 4. Se forem iguais, envia uma resposta de sucesso
    return res.json({ success: true, message: 'Acesso liberado!' });
  } else {
    // 5. Se forem diferentes, envia uma resposta de erro
    return res.json({ success: false, message: 'Token inválido.' }, 401);
  }
};
```

// ==================  
// exemplo do main.js  
// ==================  

```
module.exports = require('./index.js');
```


// =======================  
// exemplo do package.json  
// =======================  

```
{
  "dependencies": {
    "appwrite": "^11.0.0"
  }
}
```
