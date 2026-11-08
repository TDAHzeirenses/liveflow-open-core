# LiveFlow Open Core

Componentes Open Source selecionados do LiveFlow, disponibilizados sob a **Mozilla Public License v2.0 (MPL-2.0)**.

## Sobre

LiveFlow é uma aplicação desktop de arquitetura Open Core. Este repositório público contém exclusivamente os componentes autorizados para distribuição aberta:

- **`open_core/recurrence.py`** — Motor puro de recorrência, datas, serialização de regras e renderização de títulos
- **`open_core/__init__.py`** — Inicialização do núcleo público
- **`open_core/tests/test_recurrence.py`** — Testes isolados do módulo aberto

O restante do LiveFlow (interface gráfica, autenticação OAuth, integração com YouTube, banco de dados, instalador, etc.) permanece no repositório privado `TDAHzeirenses/liveflow-private` como componentes proprietários.

## Estrutura

```
liveflow-open-core/
├── open_core/
│   ├── __init__.py          # Metadados do pacote aberto (__version__ = "0.1.0")
│   ├── recurrence.py        # Motor de recorrência (MPL-2.0)
│   └── tests/
│       └── test_recurrence.py  # Testes isolados (unittest)
├── docs/
│   ├── ARCHITECTURE_OVERVIEW.md
│   ├── OPEN_CORE_MODEL.md
│   └── ARCHITECTURE_DIAGRAMS.md
├── LICENSE                  # MPL-2.0
├── THIRD-PARTY-NOTICES.md   # Notificações de dependências de terceiros
└── README.md                # Este documento
```

## Licença

Todo o código neste repositório está sob a **Mozilla Public License v2.0 (MPL-2.0)**, exceto onde indicado em contrário.

Veja `LICENSE` e `THIRD-PARTY-NOTICES.md` para detalhes.

## Uso

```python
from open_core.recurrence import RecurrenceRule, occurrences
from datetime import date, time

rule = RecurrenceRule(
    start_date=date(2026, 11, 5),
    times=[time(19)],
    frequency="daily",
    count=3,
    timezone="America/Sao_Paulo",
)

occs = occurrences(rule)
print([o.isoformat() for o in occs])
```

## Contribuição

Veja `CONTRIBUTING.md` (pendente de criação).

## Segurança

Relate vulnerabilidades através de `SECURITY.md` (pendente de criação).

---

*LiveFlow Open Core — componente aberto do ecossistema LiveFlow*
