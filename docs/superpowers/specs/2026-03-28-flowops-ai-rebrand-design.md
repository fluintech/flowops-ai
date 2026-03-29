# Design Spec: Rebrand do Fork para FlowOps AI (Sem Alterar Core)

## Contexto

O repositório atual é um fork com branding legado e o objetivo é adotar a marca da startup Fluintech, com nome oficial do produto definido como **FlowOps AI**. O pedido explicita que o core não deve ser alterado.

## Objetivo

Executar um rebrand completo de naming e identidade textual no projeto, cobrindo superfícies visíveis e documentação, preservando comportamento, arquitetura funcional e contratos técnicos existentes.

## Escopo

### Incluído

- Renomeação textual de marca em docs, metadados de UI, manifestos e labels operacionais.
- Atualização de nomes exibidos ao usuário para **FlowOps AI**.
- Atualização de identificadores nominais não funcionais quando seguro.
- Varredura final para remover referências legadas residuais.

### Não incluído

- Mudanças em lógica de negócio, APIs, rotas, middleware, autenticação ou fluxos internos.
- Refatorações estruturais não relacionadas ao rebrand.
- Mudanças visuais profundas (layout/tema) além de nome e metadados.

## Abordagem Selecionada

Foi selecionada a abordagem híbrida com mapeamento, com descoberta completa antes de editar:

1. Inventariar ocorrências de branding antigo no repositório.
2. Classificar por lotes de alteração.
3. Aplicar lotes incrementalmente com revisão entre etapas.
4. Validar integridade técnica e cobertura de branding.

Essa abordagem reduz risco de tocar identificadores sensíveis indevidamente e mantém rastreabilidade de cada mudança.

## Arquitetura de Execução

### Fase 1: Descoberta

- Buscar strings de branding e aliases legados em todo o repositório.
- Classificar cada ocorrência como:
  - Branding visível (mudar).
  - Operacional não funcional (mudar com cuidado).
  - Técnica/funcional crítica (não mudar sem validação explícita).

### Fase 2: Aplicação por lotes

#### Lote A: Documentação

- Arquivos de alto impacto: `README.md`, `ROADMAP.md`, `CONTRIBUTING.md`, `SECURITY.md`, `docs/*`.
- Objetivo: alinhar comunicação pública para **FlowOps AI**.

#### Lote B: UI e Metadados

- Título da aplicação, nome curto/longo, descrição, manifestos e labels exibidos.
- Objetivo: garantir experiência consistente de marca em app/PWA.

#### Lote C: Configuração e Operação

- `package.json` (nome e labels de scripts/processos quando não afetam runtime).
- `.env.example` e textos operacionais não funcionais.
- Objetivo: alinhar nomenclatura interna de operação.

#### Lote D: Varredura Final

- Nova busca global por termos legados.
- Revisão manual de falsos positivos.
- Confirmação de cobertura final.

## Fluxo de Dados e Decisão

1. Entrada: termos legados detectados no código/docs.
2. Classificação: branding vs técnico funcional.
3. Transformação: aplicar renomeação somente em contexto permitido.
4. Verificação: build/lint + busca residual.
5. Saída: repositório com branding atualizado para **FlowOps AI**, sem mudança de core.

## Tratamento de Risco e Ambiguidade

- Qualquer termo ambíguo será pausado para confirmação antes da alteração.
- Identificadores que possam ser usados por integrações externas serão preservados, salvo confirmação explícita.
- Mudanças serão pequenas e auditáveis por lote para facilitar rollback pontual.

## Estratégia de Testes e Verificação

- Validação estática:
  - Busca residual de termos antigos.
  - Revisão de arquivos alterados por lote.
- Validação técnica:
  - Executar `npm run lint` e `npm run build` (quando disponíveis).
- Critério de aceite:
  - Branding visível e documental totalmente em **FlowOps AI**.
  - Sem regressão de compilação/lint.
  - Sem alteração de comportamento funcional.

## Critérios de Sucesso

- Nome oficial **FlowOps AI** aplicado de forma consistente em superfícies de produto e docs.
- Core preservado, sem mudanças em comportamento.
- Mudanças rastreáveis e reversíveis por lote.

## Fora de Escopo Futuro (Backlog)

- Ajustes de identidade visual aprofundados (paleta, tipografia, logo customizada completa).
- Reposicionamento de UX/copy além de nomenclatura.
