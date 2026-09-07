# Auditoria Técnica Pré-Deploy — LPs/Sites Aline

> Antes de subir pro domínio definitivo, garantir que tudo abaixo está implementado.
> Última atualização: **2026-05-06**

---

## Resumo

| Item | Status | Bloqueia deploy? |
|---|---|---|
| Meta Pixel | Pendente | Não (mas fundamental pra ads) |
| LinkedIn Insight Tag | Pendente | Não (relevante pra LP empresarial) |
| GA4 (substituir placeholder) | Placeholder | Sim — métrica básica |
| Google Ads Conversion (substituir placeholder) | Placeholder | Sim — sem isso a campanha não otimiza |
| Schema.org LegalService | Pendente | Não (mas ajuda SEO) |
| Open Graph + Twitter Card | Pendente | Não (mas link feio quando compartilhado) |
| sitemap.xml | Pendente | Não |
| robots.txt | Pendente | Não |
| Favicon + apple-touch-icon | Pendente | Não |
| Política de Privacidade | Pendente | **Sim** — LGPD |
| Cookie banner LGPD | Pendente | **Sim** — se rodar pixel/ads |
| Canonical URLs | Pendente | Não |

---

## Implementação detalhada

### 1. Meta Pixel (Facebook + Instagram Ads)

Bloco a colar no `<head>` de cada LP:
```html
<!-- Meta Pixel -->
<script>
!function(f,b,e,v,n,t,s){...}(window, document,'script',
'https://connect.facebook.net/en_US/fbevents.js');
fbq('init', 'PIXEL_ID_AQUI');
fbq('track', 'PageView');
</script>
<noscript><img height="1" width="1" style="display:none"
  src="https://www.facebook.com/tr?id=PIXEL_ID_AQUI&ev=PageView&noscript=1"/></noscript>
```

Eventos a disparar:
- `Lead` quando clica em botão WhatsApp
- `Contact` no submit de formulário (se houver)

**Pendência:** ID do pixel — criar conta Business Manager Meta e gerar.

---

### 2. LinkedIn Insight Tag (LP empresarial principalmente)

```html
<!-- LinkedIn Insight -->
<script type="text/javascript">
_linkedin_partner_id = "PARTNER_ID_AQUI";
window._linkedin_data_partner_ids = window._linkedin_data_partner_ids || [];
window._linkedin_data_partner_ids.push(_linkedin_partner_id);
</script>
<script type="text/javascript">
(function(l) { ... })(window.lintrk);
</script>
```

**Pendência:** Partner ID — criar Campaign Manager LinkedIn.

---

### 3. GA4 + Google Ads (substituir placeholders)

Já instalado nas LPs. Substituir 3 strings em ambas:

| Placeholder | Substituir por |
|---|---|
| `G-ALINELP000` | Measurement ID GA4 |
| `AW-XXXXXXXXXX` | Conversion ID Google Ads |
| `XXXXXXXX/XXXX` | Conversion Label clique WhatsApp |

---

### 4. Schema.org JSON-LD (LegalService)

Bloco pra incluir no `<head>` do site institucional:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LegalService",
  "name": "Carlesso & Araujo Advogados",
  "image": "https://alinecarlesso.com.br/logos/logo-aline.jpeg",
  "url": "https://alinecarlesso.com.br",
  "telephone": "+55-11-XXXXXXXXX",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "ENDEREÇO DO ESCRITÓRIO",
    "addressLocality": "São Paulo",
    "addressRegion": "SP",
    "postalCode": "XXXXX-XXX",
    "addressCountry": "BR"
  },
  "priceRange": "$$$",
  "areaServed": "BR"
}
</script>
```

**Pendência:** endereço, telefone, CEP do escritório.

---

### 5. Open Graph + Twitter Card

Cada página deve ter no `<head>`:
```html
<meta property="og:type" content="website">
<meta property="og:locale" content="pt_BR">
<meta property="og:site_name" content="Carlesso & Araujo Advogados">
<meta property="og:title" content="...título da página...">
<meta property="og:description" content="...descrição...">
<meta property="og:url" content="https://...url-da-página...">
<meta property="og:image" content="https://...imagem-1200x630.jpg">

<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="...">
<meta name="twitter:description" content="...">
<meta name="twitter:image" content="https://...">
```

**Pendência:** imagens OG (1200x630px) específicas pra cada página. Pode usar logo + texto da página em primeiro momento.

---

### 6. sitemap.xml

Criar na raiz:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://DOMINIO/</loc><priority>1.0</priority></url>
  <url><loc>https://DOMINIO/site-escritorio/</loc><priority>0.9</priority></url>
  <url><loc>https://DOMINIO/site-dra-aline/</loc><priority>0.9</priority></url>
  <url><loc>https://DOMINIO/site-dra-aline/empresarial/</loc><priority>0.8</priority></url>
  <url><loc>https://DOMINIO/site-dra-aline/patrimonial/</loc><priority>0.8</priority></url>
  <url><loc>https://DOMINIO/cartao-digital/</loc><priority>0.7</priority></url>
</urlset>
```

---

### 7. robots.txt

```
User-agent: *
Allow: /

Sitemap: https://DOMINIO/sitemap.xml
```

---

### 8. Favicon + apple-touch-icon

Adicionar no `<head>` de cada página:
```html
<link rel="icon" type="image/png" href="/favicon.png">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

**Pendência:** gerar arquivos a partir da logo (180x180 e 32x32).

---

### 9. Política de Privacidade (LGPD)

**Obrigatória** se a página rodar qualquer pixel ou coletar formulário.

Estrutura mínima:
- Quem controla os dados (escritório).
- Quais dados são coletados (cookies de analytics, dados de formulário).
- Finalidade (atendimento, marketing, métricas).
- Base legal (legítimo interesse + consentimento).
- Como exercer direitos LGPD (DPO, e-mail).
- Retenção e exclusão.

**Pendência:** redigir texto completo. Pode usar template OAB-compliant e adaptar.

---

### 10. Cookie banner LGPD

Necessário se rodar pixel (Meta, Google Ads, LinkedIn). Stack mínimo: banner JS pequeno, com 2 botões (aceitar / rejeitar) e link pra política.

Opções:
- Solução pronta gratuita: CookieYes free, Cookiebot free
- DIY: ~50 linhas JS

**Decisão:** usar CookieYes free (rápido) ou implementar custom?

---

## Ordem de implementação sugerida

**Bloco 1 — agora (não depende de info externa):**
- [x] Schema.org LegalService (com placeholder de endereço/tel)
- [x] Open Graph básico (com logo padrão)
- [x] sitemap.xml + robots.txt (provisório com URLs do GitHub Pages)
- [x] Favicon + apple-touch-icon

**Bloco 2 — quando Nei criar contas de ads:**
- [ ] Meta Pixel
- [ ] LinkedIn Insight Tag
- [ ] Substituir placeholder GA4
- [ ] Substituir placeholder Google Ads Conversion

**Bloco 3 — antes do deploy final:**
- [ ] Política de Privacidade redigida
- [ ] Cookie banner LGPD ativo
- [ ] Endereço, telefone do escritório no Schema.org
- [ ] sitemap atualizado com domínio definitivo

---

## Observações

- O `cartao-digital` não precisa de pixel/cookie banner (não tem campanha de ads, só link compartilhado).
- O `site-dra-aline/index.html` (site pessoal dela) e o `site-escritorio/index.html` precisam de SEO básico (Schema, OG) mas não de pixel.
- As **LPs** são as que precisam de tudo: pixel, gtag, conversion, cookie banner.
