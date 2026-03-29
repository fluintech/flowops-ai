# FlowOps AI Rebrand Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Renomear o fork para FlowOps AI em docs, UI e metadados sem alterar comportamento do sistema.

**Architecture:** A execução será por lotes independentes (documentação, interface/metadados, config/operação e verificação final) para manter mudanças pequenas e rastreáveis. Cada lote atualiza apenas strings de branding e labels não funcionais. A validação combina busca residual de termos legados com lint/build.

**Tech Stack:** Next.js 16, React 19, TypeScript, Node.js, Markdown docs

---

## File Structure / Ownership

- `README.md`, `ROADMAP.md`, `CONTRIBUTING.md`, `SECURITY.md`, `docs/COST-TRACKING.md`: superfícies de documentação pública/operacional.
- `src/app/layout.tsx`, `src/app/login/page.tsx`, `src/app/office/page.tsx`, `src/app/(dashboard)/*`: títulos e textos de UI.
- `public/manifest.json`, `src/config/branding.ts`, `.env.example`, `package.json`: metadados de app e defaults de branding.
- `src/app/api/*` com labels textuais: nomes exibidos em checks/serviços sem mudança de lógica.

### Task 1: Inventário e Baseline de Branding

**Files:**
- Modify: `docs/superpowers/plans/2026-03-28-flowops-ai-rebrand-implementation.md` (checklist status only)
- Output: `tmp/rebrand-scan-before.txt`

- [x] **Step 1: Gerar inventário completo de termos legados**

Run:
```bash
mkdir -p tmp
rg -n "Mission Control|mission-control|MissionCtrl|TenacitOS|OpenClaw" README.md ROADMAP.md CONTRIBUTING.md SECURITY.md docs public src .env.example package.json > tmp/rebrand-scan-before.txt
```
Expected: arquivo `tmp/rebrand-scan-before.txt` criado com todas as ocorrências.

- [x] **Step 2: Confirmar baseline**

Run:
```bash
wc -l tmp/rebrand-scan-before.txt
head -n 20 tmp/rebrand-scan-before.txt
```
Expected: número de ocorrências inicial documentado para comparação final.

- [x] **Step 3: Commit**

```bash
git add tmp/rebrand-scan-before.txt docs/superpowers/plans/2026-03-28-flowops-ai-rebrand-implementation.md
git commit -m "chore: capture branding baseline scan for FlowOps AI rebrand"
```

### Task 2: Lote A - Documentação

**Files:**
- Modify: `README.md`
- Modify: `ROADMAP.md`
- Modify: `CONTRIBUTING.md`
- Modify: `SECURITY.md`
- Modify: `docs/COST-TRACKING.md`

- [ ] **Step 1: Aplicar renomeações de branding na documentação**

Run:
```bash
perl -0pi -e 's/\bMission Control\b/FlowOps AI/g; s/\bmission-control\b/flowops-ai/g; s/\bMissionCtrl\b/FlowOpsAI/g; s/\bTenacitOS\b/FlowOps AI/g' README.md ROADMAP.md CONTRIBUTING.md SECURITY.md docs/COST-TRACKING.md
```
Expected: docs refletem o novo nome e labels legados principais deixam de aparecer.

- [ ] **Step 2: Verificar somente docs**

Run:
```bash
rg -n "Mission Control|mission-control|MissionCtrl|TenacitOS" README.md ROADMAP.md CONTRIBUTING.md SECURITY.md docs/COST-TRACKING.md
```
Expected: sem resultados, exceto casos intencionais em histórico (se houver).

- [ ] **Step 3: Commit**

```bash
git add README.md ROADMAP.md CONTRIBUTING.md SECURITY.md docs/COST-TRACKING.md
git commit -m "docs: rebrand project documentation to FlowOps AI"
```

### Task 3: Lote B - UI e Metadados

**Files:**
- Modify: `public/manifest.json`
- Modify: `src/config/branding.ts`
- Modify: `src/app/layout.tsx`
- Modify: `src/app/login/page.tsx`
- Modify: `src/app/office/page.tsx`
- Modify: `src/app/(dashboard)/page.tsx`
- Modify: `src/app/(dashboard)/settings/page.tsx`
- Modify: `src/app/(dashboard)/workflows/page.tsx`
- Modify: `src/components/Sidebar.tsx`

- [ ] **Step 1: Atualizar defaults e metadados principais**

Edits:
```ts
// src/config/branding.ts
agentName: process.env.NEXT_PUBLIC_AGENT_NAME || "FlowOps AI"
companyName: process.env.NEXT_PUBLIC_COMPANY_NAME || "FLOWOPS AI"
appTitle: process.env.NEXT_PUBLIC_APP_TITLE || "FlowOps AI"
```

```json
// public/manifest.json
{
  "name": "FlowOps AI",
  "short_name": "FlowOpsAI"
}
```

- [ ] **Step 2: Atualizar strings visíveis de UI**

Run:
```bash
perl -0pi -e 's/\bMission Control\b/FlowOps AI/g; s/\bTenacitOS\b/FlowOps AI/g' src/app/layout.tsx src/app/login/page.tsx src/app/office/page.tsx src/app/\(dashboard\)/page.tsx src/app/\(dashboard\)/settings/page.tsx src/app/\(dashboard\)/workflows/page.tsx src/components/Sidebar.tsx
```
Expected: títulos, cabeçalhos e descrições visíveis exibem FlowOps AI.

- [ ] **Step 3: Commit**

```bash
git add public/manifest.json src/config/branding.ts src/app/layout.tsx src/app/login/page.tsx src/app/office/page.tsx src/app/\(dashboard\)/page.tsx src/app/\(dashboard\)/settings/page.tsx src/app/\(dashboard\)/workflows/page.tsx src/components/Sidebar.tsx
git commit -m "feat: apply FlowOps AI branding across UI metadata and labels"
```

### Task 4: Lote C - Configuração e Operação

**Files:**
- Modify: `package.json`
- Modify: `.env.example`
- Modify: `src/app/api/system/stats/route.ts`
- Modify: `src/app/api/system/monitor/route.ts`
- Modify: `src/app/api/health/route.ts`
- Modify: `src/app/(dashboard)/logs/page.tsx`
- Modify: `src/app/(dashboard)/terminal/page.tsx`
- Modify: `src/app/(dashboard)/actions/page.tsx`

- [ ] **Step 1: Atualizar nome de pacote e defaults de ambiente**

Edits:
```json
// package.json
{
  "name": "flowops-ai"
}
```

```dotenv
# .env.example
NEXT_PUBLIC_AGENT_NAME=FlowOps AI
NEXT_PUBLIC_AGENT_DESCRIPTION=Your AI co-pilot, powered by OpenClaw
NEXT_PUBLIC_APP_TITLE=FlowOps AI
```

- [ ] **Step 2: Atualizar labels operacionais sem mudar comandos/serviços**

Run:
```bash
perl -0pi -e 's/\bMission Control\b/FlowOps AI/g; s/\bmission-control\b/flowops-ai/g' src/app/api/system/stats/route.ts src/app/api/system/monitor/route.ts src/app/api/health/route.ts src/app/\(dashboard\)/logs/page.tsx src/app/\(dashboard\)/terminal/page.tsx src/app/\(dashboard\)/actions/page.tsx
```
Expected: labels e caminhos nominais mudam para FlowOps AI; lógica continua idêntica.

- [ ] **Step 3: Commit**

```bash
git add package.json .env.example src/app/api/system/stats/route.ts src/app/api/system/monitor/route.ts src/app/api/health/route.ts src/app/\(dashboard\)/logs/page.tsx src/app/\(dashboard\)/terminal/page.tsx src/app/\(dashboard\)/actions/page.tsx
git commit -m "chore: rename operational labels and package name to flowops-ai"
```

### Task 5: Lote D - Verificação Técnica e Busca Residual

**Files:**
- Output: `tmp/rebrand-scan-after.txt`

- [ ] **Step 1: Rodar busca residual global**

Run:
```bash
rg -n "Mission Control|mission-control|MissionCtrl|TenacitOS" README.md ROADMAP.md CONTRIBUTING.md SECURITY.md docs public src .env.example package.json > tmp/rebrand-scan-after.txt || true
```
Expected: arquivo vazio ou apenas referências legadas deliberadamente preservadas.

- [ ] **Step 2: Validar build/lint**

Run:
```bash
npm run lint
npm run build
```
Expected: ambos os comandos completam com sucesso.

- [ ] **Step 3: Revisar diff final e commit de fechamento**

Run:
```bash
git status --short
git diff --stat
git add -A
git commit -m "chore: finalize FlowOps AI rebrand validation"
```
Expected: estado limpo após commit final.
