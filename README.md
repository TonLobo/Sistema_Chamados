# PGMBox Suporte

> Sistema de Gestão de Chamados de Suporte — aplicação web completa em HTML/JS puro, sem dependência de servidor, pronta para uso imediato.

---

## ✨ Funcionalidades

| Módulo | Descrição |
|--------|-----------|
| **Autenticação** | Login com senha criptografada (AES-256 + PBKDF2), sessão segura, recuperação de senha por e-mail |
| **Chamados** | Fluxo completo: Aberto → Em Atendimento → Aguardando Cliente → Resolvido → Encerrado |
| **Fila de E-mails** | Recebimento automático de chamados via e-mail com fila de recategorização |
| **SLA** | Configurável por prioridade; dashboard com gráficos de cumprimento |
| **Analistas** | Perfis Admin, Consultor, Analista N1/N2/N3 com controle de acesso |
| **Consultoria** | Envio para consultoria com checklist obrigatório de requisitos mínimos |
| **Notificações** | Internas (sino) + e-mail (EmailJS) a cada mudança de status |
| **Relatório SLA** | Gráficos por mês, pizza dentro/fora prazo, ranking de analistas, filtros por período |
| **API Pública** | `window.PGMBoxAPI` para integração com sistemas externos |

---

## 🚀 Como usar

### Opção 1 — Abrir diretamente no navegador

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/pgmbox-suporte.git
cd pgmbox-suporte

# Abra o arquivo no navegador
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

### Opção 2 — GitHub Pages (recomendado)

1. Faça fork ou suba o repositório no GitHub
2. Vá em **Settings → Pages**
3. Em *Branch*, selecione `main` e pasta `/root`
4. Clique **Save** — o sistema ficará disponível em:
   `https://SEU_USUARIO.github.io/pgmbox-suporte`

### Opção 3 — Netlify Drop

1. Acesse [netlify.com/drop](https://app.netlify.com/drop)
2. Arraste a pasta do projeto
3. URL gerada instantaneamente

---

## 🔑 Acesso inicial

| Campo | Valor |
|-------|-------|
| E-mail | `everton@pgmbox.com.br` |
| Senha | `Admin@2025` |

> ⚠️ **Troque a senha imediatamente** após o primeiro acesso em **Configurações**.

---

## 🛠️ Estrutura do projeto

```
pgmbox-suporte/
├── index.html          ← Aplicação completa (self-contained)
├── README.md           ← Este arquivo
├── docs/
│   ├── manual-usuario.md          ← Manual de uso para iniciantes
│   ├── manual-email.md            ← Configuração de e-mail e SMTP
│   └── guia-integracao.md         ← Integração com sistemas externos
└── .github/
    └── ISSUE_TEMPLATE.md
```

---

## 🔌 Integração com sistemas externos

O sistema expõe uma API JavaScript acessível por qualquer script rodando na mesma página:

```javascript
// Criar chamado via API
window.PGMBoxAPI.criarChamado({
  titulo: "Erro no módulo financeiro",
  cliente: "Prefeitura de Campinas",
  prioridade: "alta",  // baixa | media | alta | critica
  descricao: "Descrição detalhada...",
  modulo: "Financeiro"
});

// Enviar e-mail para a fila de recategorização
window.PGMBoxAPI.receberEmail({
  remetente: "usuario@cliente.com.br",
  nome: "Nome do Usuário",
  assunto: "Título do problema",
  corpo: "Corpo completo do e-mail"
});

// Listar chamados
const chamados = window.PGMBoxAPI.getChamados({ status: 'aberto' });

// Mudar status de um chamado
window.PGMBoxAPI.mudarStatus('cha_123456', 'resolvido', 'Problema corrigido');
```

Consulte `docs/guia-integracao.md` para exemplos completos com webhooks, Zapier e backend Node.js.

---

## 📧 E-mail

O sistema usa [EmailJS](https://emailjs.com) para envio de notificações sem necessidade de backend.

Consulte `docs/manual-email.md` para configuração passo a passo.

---

## 🔐 Segurança

- Senhas armazenadas com **SHA-256 + PBKDF2** (100.000 iterações)
- Tokens de sessão criptografados com **AES-256-GCM**
- Nenhum dado sensível trafega para servidores externos
- Armazenamento local via `localStorage` + `sessionStorage`

> **Nota sobre produção:** para uso corporativo com múltiplos usuários simultâneos, considere migrar o `localStorage` para um backend com banco de dados (ver `docs/guia-integracao.md`).

---

## 📄 Licença

MIT — livre para uso comercial e modificação.
