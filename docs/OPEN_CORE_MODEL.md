# LiveFlow v1.0.0-rc.1 — OPEN_CORE_MODEL.md

Definição detalhada do modelo Open Core do LiveFlow.

**Status:** Documentação conceitual — sujeita à revisão jurídica
**Versão:** 1.0.0-rc.1
**Data:** 8 de novembro de 2026

---

## 1. Definição Conceitual

LiveFlow é uma aplicação desktop de arquitetura Open Core, que combina componentes proprietários responsáveis por funcionalidades estratégicas e mecanismos críticos com componentes Open Source selecionados, disponibilizados para inspeção, contribuição e reutilização conforme suas respectivas licenças.

O LiveFlow **não** é integralmente Open Source. Também **não** é integralmente proprietário. A classificação deve ser tecnicamente verificável e juridicamente consistente.

---

## 2. O Que É Proprietário (Camada A)

Os seguintes componentes são candidatos à classificação **PROPRIETÁRIA**, sujeita à confirmação jurídica e titularidade:

| Componente | Caminho | Justificativa |
|------------|---------|---------------|
| Interface gráfica principal | `app/ui.py` | Orquestração de janelas, navegação, dashboard, modais — valor comercial da UX |
| Gerenciamento de janelas | `app/ui.py` | Ciclo de vida da aplicação, encerramento — infraestrutura crítica |
| Autenticação e sessões | `app/` | OAuth Google, credenciais, tokens, DPAPI — mecanismo de segurança estratégico |
| Integração YouTube Data API | `app/` | Integração protegida com plataforma externa |
| Integração OBS | `app/` | Integração com software de transmissão — funcionalidade comercial |
| Sincronização de dados | `app/` | Mecanismo interno de sync — segredo comercial potencial |
| Sistema de atualizações | `app/` | Atualização do produto — infraestrutura comercial |
| Gerenciamento de credenciais | `app/` | Armazenamento e renovação de tokens — componente de segurança |

**Importante:** Esta lista é uma classificação proposta com base na responsabilidade arquitetural. Não constitui autorização para mover arquivos ou alterar licenças sem análise jurídica.

---

## 3. O Que É Open Source (Camada B)

Os seguintes componentes são candidatos à classificação **OPEN SOURCE**, sujeita à confirmação de licença efetiva de cada arquivo:

| Componente | Caminho | Justificativa |
|------------|---------|---------------|
| Algoritmos de recorrência | `open_core/recurrence.py` | Algoritmo genérico reutilizável, independente de interface |
| Inicialização do núcleo | `open_core/__init__.py` | Interface pública do núcleo aberto |
| Testes do núcleo | `open_core/tests/` | Testes associados a componentes abertos |
| Documentação pública | `docs/` (se aplicável) | Especificações de interfaces públicas |

**Importante:** A pasta `open_core/` **não** representa a totalidade do modelo de licenciamento. Apenas os arquivos com licença efetivamente aberta podem ser classificados como Open Source.

---

## 4. Por Que Essa Separação Existe

1. **Proteção de propriedade intelectual:** Componentes estratégicos (autenticação, integrações, sincronização) são protegidos como segredo comercial.
2. **Transparência seletiva:** Componentes genéricos e reutilizáveis (recorrência, modelos de dados) são abertos para inspeção e contribuição.
3. **Modularidade:** A separação permite evolução independente das camadas sem duplicação desnecessária.
4. **Segurança:** Credenciais e mecanismos de autenticação permanecem fechados para reduzir superfície de ataque.

---

## 5. Como as Camadas se Integram

A integração entre componentes proprietários e Open Core ocorre através de:

- **Interfaces públicas:** Contratos bem definidos entre o núcleo aberto e a aplicação desktop.
- **Contratos de dados:** Modelos compartilhados serializáveis (JSON, SQLite).
- **APIs internas:** Chamadas de função entre camadas com validação de entrada/saída.
- **Eventos:** Sistema de notificação entre componentes sem acoplamento direto.
- **Modelos compartilhados:** Estruturas de dados usadas por ambas as camadas.

**Princípio:** A separação deve permitir evolução independente, sem exposição acidental de lógica proprietária.

---

## 6. Limites de Reutilização

| Tipo de Componente | Pode ser inspecionado | Pode ser modificado | Pode ser redistribuído | Requer autorização |
|--------------------|----------------------|---------------------|------------------------|-------------------|
| Open Core (licença aberta) | Sim | Sim (conforme licença) | Sim (conforme licença) | Não |
| Proprietário | Não (código fechado) | Não | Não | Sim |
| Terceiros | Conforme licença | Conforme licença | Conforme licença | Conforme licença |

**Não prometa acesso aberto aos componentes proprietários.**

---

## 7. Licenças Aplicáveis

| Categoria | Licença | Status |
|-----------|---------|--------|
| Componentes Open Core | PENDENTE DE CONFIRMAÇÃO | Verificar arquivo LICENSE em open_core/ |
| Componentes proprietários | Licença fechada (EULA) | EULA.md existe no repositório |
| Bibliotecas de terceiros | PENDENTE DE CONFIRMAÇÃO | Inventário necessário (veja THIRD_PARTY_LICENSE_AUDIT.md) |
| Recursos gráficos (assets/) | PENDENTE DE CONFIRMAÇÃO | Verificar origem e licença de cada arquivo |

---

## 8. Posicionamento Oficial do Produto

> LiveFlow é uma aplicação desktop de arquitetura Open Core, que combina componentes proprietários responsáveis por funcionalidades estratégicas e mecanismos críticos com componentes Open Source selecionados, disponibilizados para inspeção, contribuição e reutilização conforme suas respectivas licenças.

**Não apresentar o LiveFlow como integralmente Open Source.**
**Também não apresentar o projeto como integralmente proprietário.**

---

## 9. Pendências

- Verificar existência e conteúdo de arquivo LICENSE no diretório open_core/
- Verificar cabeçalhos de copyright em todos os arquivos Python
- Inventário completo de dependências de terceiros e suas licenças
- Revisão jurídica de todas as classificações propostas
- Verificação de segredos credenciais em assets/oauth_client.json e outros arquivos

---

*Fim do OPEN_CORE_MODEL.md*
