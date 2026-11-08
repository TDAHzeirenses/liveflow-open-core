# LiveFlow v1.0.0-rc.1 — ARCHITECTURE_OVERVIEW.md

Visão geral da arquitetura, camadas, módulos, dependências e fluxo de execução do LiveFlow.

**Status:** Documentação arquitetural — baseada na inspeção do repositório RC.1
**Versão:** 1.0.0-rc.1
**Data:** 8 de novembro de 2026

---

## 1. Visão Geral

O LiveFlow é uma aplicação desktop para Windows 10/11 x64, desenvolvida em Python com interface Tkinter, adotando o modelo de arquitetura **Open Core**: componentes críticos e estratégicos são proprietários, enquanto componentes não críticos e selecionados são disponibilizados como código aberto.

A aplicação oferece gerenciamento de transmissões do YouTube, com autenticação OAuth, agendamento, sincronização, persistência local, interface gráfica com sidebar, sistema de temas e modal de doações (PIX, Bitcoin, Solana).

---

## 2. Estrutura de Diretórios

```
LiveFlow/
├── main.py                    # Ponto de entrada da aplicação
├── app/                       # Camada da aplicação desktop (interface e serviços)
│   ├── ui.py                  # Interface gráfica principal (Tkinter)
│   ├── theme_manager.py       # Gerenciamento de temas (Claro/Escuro/Automático)
│   ├── donations.py           # Modal de doações (PIX, Bitcoin, Solana)
│   └── ...                    # Outros módulos da camada app/
├── open_core/                 # Núcleo Open Core (componentes compartilháveis)
│   ├── __init__.py
│   ├── recurrence.py          # Algoritmos de recorrência e agendamento
│   ├── tests/                 # Testes associados ao núcleo
│   └── __pycache__/
├── installer/                 # Configuração de distribuição e instalação
│   ├── LiveFlow.nsi           # Script NSIS para instalador Windows
│   ├── build_installer.ps1    # Script PowerShell para build do instalador
│   ├── create_nsis_manifest.py # Gerador de manifesto NSIS
│   └── __init__.py
├── docs/                      # Documentação do projeto
├── assets/                    # Recursos gráficos e multimídia
│   ├── liveflow.ico           # Ícone da aplicação
│   ├── liveflow.png           # Imagem da aplicação
│   ├── oauth_client.json      # Cliente OAuth (client_id apenas)
│   └── private/               # Recursos privados (excluídos via .gitignore)
├── tests/                     # Testes automatizados da aplicação
├── reports/                   # Relatórios de auditoria e testes
├── .gitignore                 # Regras de exclusão do Git
├── EULA.md                    # Contrato de licença do usuário final
└── LICENSE                    # (se existir) — PENDENTE DE CONFIRMAÇÃO
```

---

## 3. Camadas Arquiteturais

### CAMADA A — PROPRIETÁRIA

Componentes críticos e estratégicos que constituem o valor comercial do produto. Candidatos à classificação proprietária:

- **Interface gráfica principal (`app/ui.py`)**: Orquestração de janelas, sidebar, navegação, dashboard, modais, formulários e integração com serviços externos.
- **Gerenciamento de janelas**: Inicialização, ciclo de vida da aplicação Tkinter, encerramento.
- **Autenticação e sessões**: OAuth Google, gerenciamento de credenciais, tokens de acesso, DPAPI.
- **Integrações protegidas**: YouTube Data API, OBS, sincronização de dados.
- **Sistema de atualizações**: Verificação e aplicação de atualizações do produto.
- **Recursos comerciais exclusivos**: Funcionalidades cuja implementação é considerada segredo comercial.

**Status:** Classificação proposta sujeita à confirmação jurídica e titularidade.

### CAMADA B — OPEN SOURCE

Componentes disponibilizados sob licenças abertas, conforme licença efetiva de cada arquivo:

- **`open_core/recurrence.py`**: Algoritmos de recorrência e agendamento genéricos.
- **`open_core/__init__.py`**: Inicialização do núcleo público.
- **`open_core/tests/`**: Testes associados ao núcleo aberto.
- **Documentação técnica pública**: Especificações de interfaces públicas.

**Status:** Classificação proposta sujeita à confirmação de licença efetiva de cada arquivo.

### CAMADA C — INTEGRAÇÃO

Interfaces públicas, contratos de dados e APIs internas que permitem comunicação entre as camadas proprietária e aberta sem exposição acidental de lógica proprietária.

---

## 4. Fluxo de Execução

```
Inicialização
    │
    ▼
main.py ──────────────────────────────────────►
    │  Carrega módulos da camada app/
    │  Configura ambiente Python/Tkinter
    │  Inicializa serviços internos (auth, sync, persistence)
    ▼
app/ui.py ─────────────────────────────────────►
    │  Cria janela principal (Tkinter)
    │  Inicializa sidebar e navegação
    │  Carrega tema (Claro/Escuro/Automático)
    │  Registra callbacks e eventos
    ▼
Loop principal Tkinter ───────────────────────►
    │  Processa eventos da interface
    │  Dispara ações de navegação, agendamento, sincronização
    │  Chama serviços internos conforme necessário
    │
    ▼
Encerramento ─────────────────────────────────►
    │  Salva persistência local
    │  Libera recursos (sessões, conexões)
    │  Finaliza processo
```

---

## 5. Principais Módulos e Responsabilidades

| Módulo | Caminho | Responsabilidade | Classificação Proposta |
|--------|---------|------------------|------------------------|
| Ponto de entrada | `main.py` | Inicialização, carregamento de módulos, configuração, tratamento de exceções | PENDENTE DE CONFIRMAÇÃO |
| Interface gráfica | `app/ui.py` | Janela principal, sidebar, navegação, dashboard, modais, formulários | PENDENTE DE CONFIRMAÇÃO |
| Gerenciador de temas | `app/theme_manager.py` | Temas Claro/Escuro/Automático, paleta de cores, regras de contraste | PENDENTE DE CONFIRMAÇÃO |
| Doações | `app/donations.py` | Modal PIX, Bitcoin, Solana, cópia de chaves, QR Code | PENDENTE DE CONFIRMAÇÃO |
| Recorrência | `open_core/recurrence.py` | Algoritmos de recorrência e agendamento | PENDENTE DE CONFIRMAÇÃO |
| Instalador NSIS | `installer/LiveFlow.nsi` | Empacotamento Windows, instalação/desinstalação | PENDENTE DE CONFIRMAÇÃO |
| Build do instalador | `installer/build_installer.ps1` | Script de construção do instalador | PENDENTE DE CONFIRMAÇÃO |

---

## 6. Dependências Principais

- **Python 3.15.0** — Runtime principal
- **PyInstaller 6.22.3** — Empacotamento de executável
- **tkinter** — Interface gráfica (biblioteca padrão Python)
- **Pillow** — Manipulação de imagens
- **tzdata** — Dados de fuso horário
- **Pillow** — Manipulação de imagens
- **pywin32** — Integração Windows (DPAPI, shell)
- **NSIS 3.13** — Instalador Windows (ferramenta de build, não runtime)

---

## 7. Limitações da Auditoria

Esta documentação é baseada na inspeção do estado atual do repositório RC.1. Várias classificações de licenciamento estão marcadas como **PENDENTE DE CONFIRMAÇÃO** porque:

- Não foi possível verificar a titularidade legal de todos os arquivos
- Não foram encontrados arquivos LICENSE/LICENSE-* explícitos em todos os diretórios
- Cabeçalhos de copyright não foram verificados em todos os módulos
- Dependências de terceiros precisam de inventário completo de licenças

**Recomendação:** Revisão jurídica antes de qualquer publicação oficial de componentes como Open Source.

---

*Fim do ARCHITECTURE_OVERVIEW.md*
