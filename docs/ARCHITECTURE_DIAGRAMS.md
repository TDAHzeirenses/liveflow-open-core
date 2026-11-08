# LiveFlow v1.0.0-rc.1 — Diagrama Arquitetural (Mermaid)

Diagramas refletindo a arquitetura real do repositório RC.1.

---

## 1. Arquitetura Geral do LiveFlow

```mermaid
graph TD
    %% Pontos de entrada e camadas superiores
    User[Usuário Final] --> UI[Janela Principal Tkinter<br/>app/ui.py]
    
    %% Camada de interface
    UI --> Sidebar[Sidebar e Navegação<br/>app/ui.py]
    UI --> Dashboard[Dashboard<br/>app/ui.py]
    UI --> Themes[Tema Claro/Escuro/Auto<br/>app/theme_manager.py]
    UI --> Donations[Modal Doações PIX/BTC/SOL<br/>app/donations.py]
    
    %% Camada de serviços
    UI --> Auth[Autenticação OAuth Google<br/>app/]
    UI --> Sync[Sincronização de Dados<br/>app/]
    UI --> Sched[Agendamento Transmissões<br/>app/]
    UI --> YT[YouTube Data API<br/>app/]
    UI --> OBS[Integração OBS<br/>app/]
    UI --> Persist[Persistência Local SQLite/DPAPI<br/>app/]
    UI --> Update[Sistema de Atualizações<br/>app/]
    UI --> Diag[Diagnósticos<br/>app/]
    
    %% Núcleo Open Core
    UI --> Core[open_core/recurrence.py<br/>Algoritmos de Recorrência]
    
    %% Recursos
    UI --> Assets[assets/<br/>liveflow.ico, liveflow.png,<br/>oauth_client.json]
    
    %% Executável e instalador
    PyInstaller[PyInstaller 6.22.3] --> EXE[LiveFlow.exe]
    NSIS[NSIS 3.13] --> Installer[LiveFlow-Setup-x64.exe]
    
    classDef proprietary fill:#ffcccc,stroke:#ff0000,stroke-width:2px;
    classDef opensource fill:#ccffcc,stroke:#00ff00,stroke-width:2px;
    classDef thirdparty fill:#ccccff,stroke:#0000ff,stroke-width:1px;
    classDef integration fill:#ffffcc,stroke:#ffaa00,stroke-width:2px;
    
    class UI,Auth,Sync,Sched,YT,OBS,Persist,Update,Diag proprietary;
    class Core opensource;
    class PyInstaller,NSIS thirdparty;
    class Sidebar,Dashboard,Themes,Donations integration;
```

---

## 2. Separação entre Componentes Proprietários e Open Source

```mermaid
graph TD
    subgraph CAMADA_A["CAMADA A — PROPRIETÁRIA<br/>(Código Fechado, Acesso Controlado)"]
        UI[Interface Gráfica Principal<br/>app/ui.py]
        Auth[Autenticação e Sessões<br/>OAuth, Tokens, DPAPI]
        Sync[Sincronização de Dados<br/>Mecanismo Interno]
        Ext[Integrações Protegidas<br/>YouTube API, OBS]
        Update[Sistema de Atualizações<br/>Distribuição Comercial]
    end
    
    subgraph CAMADA_B["CAMADA B — OPEN SOURCE<br/>(Licença Aberta, Inspecionável)"]
        Recurrence[Algoritmos de Recorrência<br/>open_core/recurrence.py]
        CoreInit[Inicialização do Núcleo<br/>open_core/__init__.py]
        CoreTests[Testes do Núcleo<br/>open_core/tests/]
    end
    
    subgraph CAMADA_C["CAMADA C — INTEGRAÇÃO<br/>(Interfaces Públicas e Contratos)"]
        PublicAPI[Interfaces Públicas]
        DataContracts[Contratos de Dados<br/>JSON, SQLite]
        InternalAPI[APIs Internas]
        Events[Eventos e Callbacks]
        SharedModels[Modelos Compartilhados]
    end
    
    %% Fluxo de integração
    CAMADA_A <--> |Interfaces Públicas| CAMADA_C
    CAMADA_C <--> |Contratos de Dados| CAMADA_B
    
    %% Restrições
    CAMADA_B -.->|Não acessa diretamente<br/>lógica proprietária| CAMADA_A
    
    classDef proprietary fill:#ffcccc,stroke:#ff0000,stroke-width:2px;
    classDef opensource fill:#ccffcc,stroke:#00ff00,stroke-width:2px;
    classDef integration fill:#ffffcc,stroke:#ffaa00,stroke-width:2px;
    
    class UI,Auth,Sync,Ext,Update proprietary;
    class Recurrence,CoreInit,CoreTests opensource;
    class PublicAPI,DataContracts,InternalAPI,Events,SharedModels integration;
```

---

## 3. Comunicação entre as Camadas

```mermaid
sequenceDiagram
    participant U as Usuário
    participant UI as Interface (app/ui.py) — Proprietária
    participant C as Camada C — Integração
    participant OC as open_core/ — Open Source
    participant S as Serviços Externos<br/>(YouTube, OBS, Google OAuth)
    
    U->>UI: Ação na interface
    UI->>C: Chamada via interface pública
    C->>OC: Executa algoritmo aberto<br/>(ex: recorrência)
    OC-->>C: Retorna resultado
    C->>UI: Retorna dados via contrato
    
    alt Operação crítica
        UI->>S: Autenticação/Sync<br/>(Proprietário)
        S-->>UI: Resposta
    end
    
    UI->>U: Atualiza interface
    
    note over UI,OC: A camada Open Core não acessa<br/>diretamente a camada proprietária
```

---

## 4. Fluxo de Inicialização

```mermaid
flowchart TD
    Start([Início]) --> Main[main.py<br/>Ponto de Entrada]
    Main --> Config[Configuração do Ambiente Python]
    Config --> Load[Carregamento de Módulos<br/>app/, open_core/]
    Load --> Services[Inicialização de Serviços Internos<br/>Auth, Sync, Persistência]
    Services --> UI[Criação da Janela Principal Tkinter<br/>app/ui.py]
    UI --> Themes[Carregamento do Tema<br/>app/theme_manager.py]
    Themes --> Sidebar[Inicialização da Sidebar<br/>Navegação]
    Sidebar --> Loop[Loop Principal Tkinter]
    Loop --> Events[Processamento de Eventos]
    Events --> Actions[Ações: Navegação, Agendamento,<br/>Sincronização, Doações]
    Actions --> Services
    Actions --> UI
    
    classDef startup fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    class Main,Config,Load,Services,UI,Themes,Sidebar,Loop,Events,Actions startup;
```

---

## 5. Dependências Principais

```mermaid
graph LR
    subgraph Runtime["Runtime"]
        Python[Python 3.15.0<br/>PSFL]
        Tkinter[tkinter<br/>PSFL]
        Pillow[Pillow<br/>PIL License]
        TZ[tzdata<br/>MIT/Apache]
        PyWin[pywin32<br/>BSD-like]
    end
    
    subgraph Build["Ferramentas de Build"]
        PyInstaller[PyInstaller 6.22.3<br/>GPL/LGPL]
        NSIS[NSIS 3.13<br/>zlib/libpng]
    end
    
    subgraph App["Aplicação LiveFlow"]
        Main[main.py]
        AppUI[app/ui.py]
        Core[open_core/]
    end
    
    Python --> Main
    Tkinter --> AppUI
    Pillow --> AppUI
    TZ --> Main
    PyWin --> Main
    PyInstaller --> Main
    NSIS --> AppUI
    
    classDef runtime fill:#e8f5e9,stroke:#2e7d32,stroke-width:1px;
    classDef build fill:#fff3e0,stroke:#ef6c00,stroke-width:1px;
    classDef app fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px;
    
    class Python,Tkinter,Pillow,TZ,PyWin runtime;
    class PyInstaller,NSIS build;
    class Main,AppUI,Core app;
```

---

## 6. Observações sobre os Diagramas

- Esses diagramas refletem a **estrutura real** observada no repositório RC.1, não uma arquitetura idealizada.
- Classificações como "Proprietário" e "Open Source" são **propostas sujeitas à confirmação jurídica**.
- A pasta `open_core/` não representa a totalidade do modelo de licenciamento.
- Arquivos em `assets/private/` são excluídos do versionamento via `.gitignore`.

---

*Fim dos diagramas arquiteturais*
