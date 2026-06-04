# MoneyPrinterTurbo 💸

## Descrição

Gera vídeos curtos automaticamente com um clique usando LLMs. Você fornece o tema, ele escreve o roteiro, busca imagens/vídeos, adiciona narração e legendas — entrega pronto para TikTok, Reels e YouTube Shorts.

## Funcionalidades 🎯

- Arquitetura MVC clara e fácil manutenção.
- Suporte a geração de roteiro via IA (OpenAI, AIHubMix, Gemini, etc.).
- Várias resoluções HD (Portrait 9:16, Landscape 16:9).
- Geração de cópia customizada ou automática.
- Processamento em lote.
- Controle de duração dos clipes.
- Suporte a múltiplas vozes com pré‑visualização em tempo real.
- Legendas configuráveis (fonte, posição, cor, tamanho, contorno).
- Música de fundo (aleatória ou personalizada) com controle de volume.
- Fontes de material de alta definição e royalty‑free; é possível usar arquivos locais.
- Integração com diversos provedores de modelo (OpenAI, AIHubMix, Azure, Gemini, Ollama, etc.).

## Demonstrações de vídeo 📺

*(Imagens já presentes no README original)*

## Requisitos do Sistema 📦

- **Plataformas:** Windows 10+, macOS 11+, ou Linux.
- **CPU:** 4 cores (mínimo) – 6‑8 cores recomendado.
- **RAM:** 4 GB (mínimo) – 8 GB recomendado.
- **GPU:** Não obrigatório, mas recomendado ≥ 4 GB VRAM para aceleração.

## Guia de Início Rápido 🚀

### 1. Preparação do ambiente
| Sistema | Passo recomendado |
|--------|-------------------|
| **Windows** | Use o *one‑click package* (v1.2.6) → baixe, execute `update.bat` e depois `start.bat`. Alternativamente siga o **Deploy Manual** abaixo. |
| **macOS / Linux** | Instale **uv** → `uv python install 3.11` → `uv sync --frozen`. |
| **Docker** | `docker compose up` (ou `docker compose up` se o Docker já inclui o plug‑in). |

> **Obs.:** O workspace está em `c:\Users\useca\workspace\MoneyPrinterTurbo`.

### 2. Configurando `config.toml`
1. Copie o exemplo:
```powershell
copy config.example.toml config.toml
```
2. Edite `config.toml` e preencha os campos principais:
```toml
pexels_api_keys = ["SUA_CHAVE"]
llm_provider = "aihubmix"
aihubmix_api_key = "SUA_CHAVE"
voice_name = "pt-BR-EmilyNeural"   # opcional, para Azure TTS
subtitle_provider = "edge"          # "edge" (rápido) ou "whisper" (preciso)
# [app]
# ffmpeg_path = "C:\\caminho\\ffmpeg.exe"  # se necessário
```
3. Salve o arquivo.

### 3. Executando a **Web UI**
- **Windows**
```powershell
.\webui.bat
```
- **macOS / Linux**
```bash
sh webui.sh
# ou, se o venv já está ativo:
uv run streamlit run ./webui/Main.py --browser.gatherUsageStats=False
```
> Para acesso remoto, defina `set MPT_WEBUI_HOST=0.0.0.0` antes de iniciar.

A UI abrirá em `http://127.0.0.1:8501` (Chrome/Edge recomendado).

### 4. Usando a **API** (opcional)
```bash
uv run python main.py
```
- Docs interativos: `http://127.0.0.1:8080/docs`.
- OpenAPI (Redoc): `http://127.0.0.1:8080/redoc`.

### 5. Fluxo típico de criação de vídeo
1. Informe o tema (ex.: “Dicas de estudo”).
2. Selecione idioma e voz.
3. Escolha o formato (Portrait 9:16 ou Landscape 16:9).
4. Clique **Generate** → o sistema gera roteiro, busca material, sintetiza áudio, cria legendas e monta o vídeo HD.
5. Baixe o `*.mp4` – pronto para TikTok, Reels ou Shorts.

### 6. Dicas avançadas
| Tema | Como habilitar |
|------|----------------|
| **Múltiplas vozes** | Ajuste `voice_name` no `config.toml` ou escolha via dropdown na UI. |
| **Música de fundo personalizada** | Substitua/adicione arquivos em `resource/songs`. |
| **Fontes de legenda customizadas** | Coloque `.ttf/.otf` em `resource/fonts`. |
| **Processamento mais rápido** | Instale GPU + drivers + `ffmpeg` + `faster-whisper` (baixe modelo `large‑v3`). |
| **Deploy em nuvem** | Use o contêiner Docker em AWS/GCP/Azure. |

### 7. Solução de problemas comuns
- **`RuntimeError: No ffmpeg exe could be found`** – Instale ffmpeg e configure `[app] ffmpeg_path`.
- **Erro ao baixar modelo Whisper** – Faça download manual (Baidu/Quark) e coloque a pasta em `MoneyPrinterTurbo/models/whisper-large-v3`.
- **Limite de arquivos aberto** – Aumente `ulimit -n` (Linux/macOS) ou ajuste o registro de Windows.

### 8. Onde encontrar mais detalhes
- **README completo** – [README-en.md](file:///c:/Users/useca/workspace/MoneyPrinterTurbo/README-en.md)
- **Licença** – [LICENSE](file:///c:/Users/useca/workspace/MoneyPrinterTurbo/LICENSE)
- **Lista de vozes** – `docs/voice-list.txt`

---

**Próximos passos**
1. Configure `config.toml` com suas chaves de API.
2. Execute `webui.bat` (ou script equivalente).
3. Gere um vídeo de teste.
4. Explore a API se quiser integrar a outras aplicações.

Qualquer dúvida adicional, estou à disposição!
