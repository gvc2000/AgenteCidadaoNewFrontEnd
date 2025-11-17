# Deploy no Railway.com

Este guia mostra como fazer deploy da aplicação Agente Cidadão no Railway.com.

## 🚀 Opção 1: Deploy via GitHub (Recomendado)

### Passo 1: Push para o GitHub
```bash
git add .
git commit -m "Adicionar configuração para deploy no Railway"
git push origin main
```

### Passo 2: Deploy no Railway
1. Acesse [railway.app](https://railway.app)
2. Faça login com sua conta GitHub
3. Clique em **"New Project"**
4. Selecione **"Deploy from GitHub repo"**
5. Escolha o repositório `AgenteCidadaoFrontEnd`
6. O Railway detectará automaticamente o `package.json` e fará o build

### Passo 3: Configurar Domínio
1. Após o deploy, vá em **Settings** → **Networking**
2. Clique em **Generate Domain**
3. Copie a URL gerada (ex: `agente-cidadao-production.up.railway.app`)

## 🔧 Opção 2: Deploy via Railway CLI

### Instalar Railway CLI
```bash
npm install -g @railway/cli
```

### Login e Deploy
```bash
railway login
railway init
railway up
```

## 📋 Variáveis de Ambiente (Opcional)

Se necessário, configure no Railway:
- `PORT` - Porta do servidor (Railway configura automaticamente)
- `NODE_ENV` - Ambiente (production/development)

## 🌐 URLs Disponíveis

Após o deploy, você terá acesso a:
- `/` ou `/bilingual` - Interface bilíngue (principal)
- `/index` - Interface original em português
- `/demo` - Demo automática
- `/admin` - Painel administrativo
- `/login` - Página de login
- `/health` - Health check

## 🔍 Verificar Deploy

Acesse a URL do health check:
```
https://seu-projeto.up.railway.app/health
```

Deve retornar:
```json
{
  "status": "ok",
  "timestamp": "2025-11-17T..."
}
```

## 🐛 Troubleshooting

### Build falhou
- Verifique se o `package.json` está na raiz do projeto
- Confirme que `node_modules` está no `.gitignore`

### Aplicação não inicia
- Verifique os logs no Railway Dashboard
- Certifique-se de que a porta está configurada corretamente (`process.env.PORT`)

### CORS errors
- O servidor já está configurado com CORS habilitado
- Verifique se o webhook Railway aceita requisições da sua aplicação

## 📞 Webhook Integration

A aplicação já está configurada para enviar dados para:
```
https://primary-production-8bd9b.up.railway.app/webhook/a9eab32c-4933-4ac5-a853-879cdded3f87
```

Certifique-se de que o webhook está ativo e aceita requisições POST com JSON.

## 🔄 Atualizações

Para atualizar a aplicação:
```bash
git add .
git commit -m "Sua mensagem"
git push origin main
```

O Railway fará o redeploy automaticamente.
