
COMO CRIAR CLAUDE CODE VIA OPENROUTER NO GOOGLE Cloud Shell

Claude Haiku 4.5:
Vou ajudá-lo a entender como criar e usar Claude via OpenRouter no Google Cloud Shell. Deixe-me buscar informações atualizadas sobre isso.
Perfeito! Agora tenho informações atualizadas. Vou organizar um guia completo para você.

## Como Criar e Usar Claude Code via OpenRouter no Google Cloud Shell

**O Google Cloud Shell é um ambiente Linux baseado em navegador que oferece acesso terminal para gerenciar seus recursos na Google Cloud. Você pode configurar Claude Code com OpenRouter nele para ter um assistente de IA para coding completamente funcional na nuvem.**

---

## Processo de Configuração Passo a Passo

### 1. **Obter sua Chave de API do OpenRouter**

**Acesse** https://openrouter.ai e crie uma conta gratuita. Depois:

1. Navegue até a seção **"API Keys"**
2. Clique em **"Create Key"** e copie sua chave (começa com `sk-or-v1-`)
3. Mantenha-a segura — você usará em breve

---

### 2. **Instalar Claude Code no Cloud Shell**

Depois que o Cloud Shell abrir, execute um destes comandos:

**Opção A: Instalação nativa com curl (recomendada)**
```bash
curl -fsSL https://cli.anthropic.com/install.sh | sh
```

**Opção B: Instalação com npm** (se Node.js já estiver disponível)
```bash
npm install -g @anthropic-ai/claude-code
```

**Verificar instalação:**
```bash
claude --version
```

---

### 3. **Configurar Claude Code com OpenRouter**

Você tem **duas formas principais** de configurar. Escolha uma:

#### **Método A: Variáveis de Ambiente (mais simples)**

No Cloud Shell, adicione essas variáveis ao seu perfil shell:

```bash
nano ~/.bashrc
```

Adicione estas linhas ao final do arquivo:

```bash
export OPENROUTER_API_KEY="seu-openrouter-api-key-aqui"
export ANTHROPIC_BASE_URL="https://openrouter.ai/api"
export ANTHROPIC_AUTH_TOKEN="$OPENROUTER_API_KEY"
export ANTHROPIC_API_KEY=""  # Importante: deixar vazio
export ANTHROPIC_MODEL="meta-llama/llama-3.3-70b-instruct"
```

Salve com `Ctrl + O`, Enter, `Ctrl + X`

Recarregue o shell:
```bash
source ~/.bashrc
```

#### **Método B: Arquivo de Configuração settings.json**

Crie o arquivo de configuração:

```bash
mkdir -p ~/.claude
nano ~/.claude/settings.json
```

Cole este conteúdo (substitua sua chave OpenRouter):

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "seu-openrouter-api-key-aqui",
    "ANTHROPIC_API_KEY": "",
    "ANTHROPIC_MODEL": "meta-llama/llama-3.3-70b-instruct"
  }
}
```

Salve com `Ctrl + O`, Enter, `Ctrl + X`

---

## Modelos Livres Disponíveis no OpenRouter

| **Modelo** | **Qualidade** | **Velocidade** | **Melhor Para** |
|-----------|--------------|---------------|-----------------|
| `meta-llama/llama-3.3-70b-instruct` | Muito boa | Média | Coding complexo, raciocínio |
| `meta-llama/llama-3.1-8b-instruct` | Boa | Rápida | Tarefas simples, prototipagem |
| `google/gemini-flash-1.5-8b` | Boa | Muito rápida | Edições rápidas, sugestões |
| `google/gemini-flash-1.5` | Excelente | Média | Geral, bom equilíbrio |
| `deepseek-r1` | Excelente | Média-Lenta | Debugging, problemas complexos |

---

## Executar Claude Code no Cloud Shell

Navegue para seu projeto e inicie:

```bash
cd /path/to/seu/projeto
claude
```

**Teste com um comando simples:**
```
Crie um script Python que imprime "Olá, Cloud Shell!"
```

Se o modelo responder → **configuração bem-sucedida!** ✅

---

## Pontos Importantes para Cloud Shell

| **Aspecto** | **Detalhes** |
|-----------|----------|
| **Sessões Temporárias** | Cloud Shell desconecta após 20 minutos de inatividade. Suas configurações em `~/.bashrc` persistem entre sessões. |
| **Armazenamento** | Você tem 5 GB de armazenamento permanente em `$HOME`. Os arquivos de projeto devem ser salvos lá. |
| **Limite de Taxa** | OpenRouter free tier: ~20-50 requisições/minuto. Cloud Shell continua funcionando normalmente. |
| **Variáveis Sensíveis** | Nunca execute `claude` sem a chave configurada em variáveis de ambiente — ninguém verá suas credenciais em logs públicos do Cloud. |

---

## Resolução de Problemas Comuns

**Erro: "Auth failed" ou "401 Unauthorized"**
- Verifique se `ANTHROPIC_API_KEY` está **vazio** (não removido, mas vazio)
- Verifique se a chave OpenRouter começa com `sk-or-v1-`

**Erro: "Model not found"**
- A variável `ANTHROPIC_MODEL` deve ser exatamente um nome de modelo OpenRouter
- Modelos com `:free` (como `llama-3.3-70b:free`) **não funcionam** com Claude Code

**Claude não responde ou responde lentamente**
- Modelos menores (8B) são mais rápidos
- Modelos maiores (70B) são mais potentes mas mais lentos
- Você ultrapassou o limite de taxa? Aguarde ou altere o modelo

**As configurações desaparecem após logout**
- Certifique-se de que as variáveis estão em `~/.bashrc` (não em uma janela do terminal apenas)
- Execute `source ~/.bashrc` após cada logout/login

---

## Dicas de Produtividade

### Criar múltiplos "modos" de uso:

Você pode adicionar aliases ao seu `~/.bashrc` para alternar rapidamente entre modelos:

```bash
alias claude-fast='export ANTHROPIC_MODEL="google/gemini-flash-1.5-8b" && claude'
alias claude-powerful='export ANTHROPIC_MODEL="meta-llama/llama-3.3-70b-instruct" && claude'
alias claude-reasoning='export ANTHROPIC_MODEL="deepseek-r1" && claude'
```

Agora você pode simplesmente digitar `claude-powerful` para rodar Claude Code com o modelo mais potente.

---

**Com essa configuração, você terá um assistente de IA para coding completamente funcional no Google Cloud Shell, sem precisar pagar pela API do Anthropic!** 🚀
