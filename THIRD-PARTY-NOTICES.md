# LiveFlow v1.0.0-rc.1 — THIRD_PARTY_LICENSE_AUDIT.md

Inventário de dependências externas e suas respectivas licenças e obrigações.

**Status:** Inventário técnico — licenças de terceiros sujeitas à confirmação
**Versão:** 1.0.0-rc.1
**Data:** 8 de novembro de 2026

---

## 1. Dependências de Runtime

| Dependência | Versão | Tipo | Licença (suposta) | Obrigações de Redistribuição | Classificação |
|-------------|--------|------|-------------------|------------------------------|---------------|
| Python | 3.15.0 | Runtime | PSFL (Python Software Foundation License) | Manter avisos de copyright da PSF | TERCEIROS |
| tkinter | — | Biblioteca padrão Python | PSFL | Parte do Python, sem obrigações adicionais | TERCEIROS |
| Pillow | — | Biblioteca de imagens | PIL License | Manter aviso de copyright do Pillow | TERCEIROS |
| tzdata | — | Dados de fuso horário | MIT ou Apache 2.0 | Manter aviso de copyright | TERCEIROS |
| pywin32 | — | Extensões Windows | BSD-like | Manter aviso de copyright | TERCEIROS |

---

## 2. Dependências de Build

| Dependência | Versão | Tipo | Licença (suposta) | Obrigações de Redistribuição | Classificação |
|-------------|--------|------|-------------------|------------------------------|---------------|
| PyInstaller | 6.22.3 | Ferramenta de build | GPL v2+ com exceção de linking | Não afeta o runtime distribuído | TERCEIROS |
| NSIS | 3.13 | Ferramenta de instalador | zlib/libpng | Manter aviso de copyright | TERCEIROS |

---

## 3. Recursos Gráficos e Multimídia

| Recurso | Caminho | Origem | Licença | Obrigações | Classificação |
|---------|---------|--------|---------|------------|---------------|
| Ícone da aplicação | `assets/liveflow.ico` | PENDENTE | PENDENTE | Verificar origem e licença | PENDENTE DE CONFIRMAÇÃO |
| Imagem da aplicação | `assets/liveflow.png` | PENDENTE | PENDENTE | Verificar origem e licença | PENDENTE DE CONFIRMAÇÃO |
| QR Code PIX | `assets/private/qr-code-pix.png` | PENDENTE | PENDENTE | Pasta privada, excluída do Git | PENDENTE DE CONFIRMAÇÃO |
| Cliente OAuth | `assets/oauth_client.json` | Google (client_id) | PENDENTE | Não contém secret, mas requer verificação | PENDENTE DE CONFIRMAÇÃO |

---

## 4. Arquivos de Licença Existentes

| Arquivo | Caminho | Conteúdo | Status |
|---------|---------|----------|--------|
| EULA | `EULA.md` | Contrato de licença do usuário final | Existe no repositório |
| LICENSE | `LICENSE` | PENDENTE | Não verificado se existe |
| LICENSE-MPL-2.0.txt | PENDENTE | PENDENTE | Não verificado se existe |
| LICENSE-PROPRIETARY.txt | PENDENTE | PENDENTE | Não verificado se existe |
| LICENSES-THIRD-PARTY.txt | PENDENTE | PENDENTE | Não verificado se existe |
| THIRD-PARTY-NOTICES.txt | PENDENTE | PENDENTE | Não verificado se existe |

**Pendência:** Verificar existência e conteúdo de todos os arquivos LICENSE* e THIRD-PARTY* no repositório.

---

## 5. Obrigações de Redistribuição

### 5.1 Para componentes Open Source (se confirmados)

- Manter avisos de copyright originais
- Incluir cópia da licença em distribuições
- Indicar modificações feitas (se exigido pela licença)
- Não remover avisos de licença de terceiros

### 5.2 Para componentes proprietários

- Não redistribuir sem autorização
- Não modificar sem autorização
- Respeitar EULA.md para uso do produto

### 5.3 Para bibliotecas de terceiros

- Cada biblioteca tem sua própria licença
- Verificar compatibilidade entre licenças
- Incluir avisos de copyright obrigatórios
- Respeitar obrigações de copyleft (se aplicável)

---

## 6. Inconsistências e Pendências Identadas

1. **Arquivos LICENSE* não verificados:** Não foi possível confirmar se existem arquivos LICENSE, LICENSE-MPL-2.0.txt, LICENSE-PROPRIETARY.txt, LICENSES-THIRD-PARTY.txt ou THIRD-PARTY-NOTICES.txt no repositório.

2. **Licenças supostas:** As licenças listadas para bibliotecas de terceiros (PSFL, PIL, MIT, Apache, BSD) são baseadas em conhecimento geral e precisam ser verificadas contra os arquivos reais de licença ou cabeçalhos de código.

3. **Recursos gráficos:** Origem e licença de `liveflow.ico`, `liveflow.png` e outros assets não verificadas.

4. **Pasta `assets/private/`:** Conteúdo não inspecionado, excluído do Git via `.gitignore`.

5. **Arquivo `oauth_client.json`:** Contém `client_id` apenas (sem secret), mas ainda requer verificação de licença antes de publicação.

---

## 7. Recomendações

1. Executar varredura de licenças em todas as dependências Python (`pip-licenses` ou similar)
2. Verificar existência de arquivos LICENSE* no repositório
3. Criar arquivo THIRD-PARTY-NOTICES.txt se não existir
4. Adicionar cabeçalhos de copyright em todos os arquivos Python
5. Revisão jurídica antes de qualquer distribuição oficial

---

*Fim do THIRD_PARTY_LICENSE_AUDIT.md*
