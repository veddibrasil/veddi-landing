# VEDDI Landing Page

Site público de marketing do VEDDI — HTML/CSS/JS puro, sem dependências de build.

## Estrutura

```
veddi-landing/
  index.html          ← página principal
  assets/
    css/style.css     ← estilos
    js/main.js        ← interatividade (navbar mobile, FAQ, fade-in)
    images/           ← logos e imagens (copiar do projeto Laravel)
  nginx.conf          ← configuração do servidor web
```

## Imagens necessárias

Copiar do projeto Laravel (`public/`):

```bash
cp /caminho/para/mistercoxinha/public/logo_roxa.png  assets/images/
cp /caminho/para/mistercoxinha/public/logo_branca.png assets/images/
cp /caminho/para/mistercoxinha/public/favicon/favicon.ico assets/images/
```

## Desenvolvimento local

Abrir direto no browser ou usar um servidor estático:

```bash
# Python (mais simples)
python3 -m http.server 3000

# Node.js (npx)
npx serve .

# VS Code: instale a extensão "Live Server" e clique em "Go Live"
```

Acesse: http://localhost:3000

## Deploy no VPS

### 1. Copiar arquivos

```bash
# Via SCP
scp -r . user@SEU_IP:/var/www/veddi-landing

# Ou clonar via git no servidor
git clone https://github.com/seu-usuario/veddi-landing /var/www/veddi-landing
```

### 2. Configurar nginx

```bash
# Copiar configuração
sudo cp /var/www/veddi-landing/nginx.conf /etc/nginx/sites-available/veddi-landing
sudo ln -s /etc/nginx/sites-available/veddi-landing /etc/nginx/sites-enabled/

# Testar e recarregar
sudo nginx -t
sudo systemctl reload nginx
```

### 3. SSL com Let's Encrypt

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d veddi.com.br -d www.veddi.com.br
```

### 4. Permissões

```bash
sudo chown -R www-data:www-data /var/www/veddi-landing
sudo chmod -R 755 /var/www/veddi-landing
```

## Atualizações

```bash
# No servidor, dentro do diretório do projeto
git pull origin main
# Sem necessidade de rebuild — nginx serve os arquivos diretamente
```

## Personalização

- **URL do app**: Substituir `https://app.veddi.com.br/cadastro` pelo domínio real do app Laravel
- **Logos**: Adicionar `assets/images/logo_roxa.png` e `assets/images/logo_branca.png`
- **Preços**: Editar diretamente no `index.html` se os planos mudarem
- **Open Graph image**: Adicionar `assets/images/og-image.png` (1200×630px)
