# ERP Perfumes

Sistema de gestão para loja de perfumes.  
Interface hospedada no GitHub Pages · Dados no Google Sheets · API no Google Apps Script.

---

## Estrutura do projeto

```
/
├── Index.html          ← Interface completa (hospedada no GitHub Pages)
├── Auth.gs, Clientes.gs, Compras.gs, Dashboard.gs ...  (Google Apps Script)
├── WebApp.gs           ← Roteador HTTP (novo)
└── appsscript.json     ← Configuração do projeto
```

---

## Deploy passo a passo

### 1. Configurar o Google Apps Script

1. Acesse script.google.com e crie um novo projeto
2. Copie todos os arquivos `.gs` (um por aba)
3. Rode `inicializarSistema()` uma vez para criar as abas no Sheets

### 2. Fazer deploy como Web App

1. Clique em **Implantar → Novo deployment**
2. Tipo: **App da Web**
3. Executar como: **Eu (seu email)**
4. Quem pode acessar: **Qualquer pessoa**
5. Copie a URL gerada (formato: `https://script.google.com/macros/s/XXXX/exec`)

### 3. Configurar a URL no Index.html

No topo do script em `Index.html`:

```javascript
var API_URL = 'COLE_AQUI_A_URL_DO_WEB_APP';
// Trocar por:
var API_URL = 'https://script.google.com/macros/s/SUA_URL_AQUI/exec';
```

### 4. Subir para o GitHub

```bash
git init
git add .
git commit -m "primeiro deploy"
git remote add origin https://github.com/SEU_USUARIO/SEU_REPO.git
git push -u origin main
```

### 5. Ativar GitHub Pages

1. Settings → Pages
2. Source: Deploy from a branch → main → / (root) → Save
3. Aguarde ~2 minutos

### 6. Configurar dominio personalizado

**No GitHub Pages (Settings → Pages):**
- Custom domain: `sistema.seudominio.com.br` → Save
- Marque "Enforce HTTPS"

**No painel do registrador (subdominio recomendado):**
```
Tipo:  CNAME
Nome:  sistema
Valor: SEU_USUARIO.github.io
```

**Para dominio raiz:**
```
Tipo: A  Nome: @  Valor: 185.199.108.153
Tipo: A  Nome: @  Valor: 185.199.109.153
Tipo: A  Nome: @  Valor: 185.199.110.153
Tipo: A  Nome: @  Valor: 185.199.111.153
```

### 7. Atualizar ORIGENS_PERMITIDAS no WebApp.gs

```javascript
var ORIGENS_PERMITIDAS = [
  'https://SEU_USUARIO.github.io',
  'https://seudominio.com.br',
];
```

Depois faca novo deployment: Implantar → Gerenciar deployments → editar → nova versao.

---

## Atualizacoes

**Index.html:** `git add . && git commit -m "msg" && git push`  
GitHub Pages atualiza em ~1 minuto automaticamente.

**Arquivos .gs:** Sempre criar nova versao do deployment apos editar.

---

## Problemas comuns

- **Erro de CORS:** verifique ORIGENS_PERMITIDAS e faca novo deployment
- **API_URL nao configurada:** substitua o placeholder no Index.html
- **Mudancas no .gs nao aparecem:** crie nova versao do deployment
- **Tela em branco:** Index.html deve estar na raiz do repositorio
