# agents-claude

Repositório de agentes especializados para o Claude Code, organizados em um fluxo de trabalho PO → QA → DEV.

Cada agente tem uma responsabilidade única e bem delimitada. O output de um alimenta o input do próximo, garantindo que requisitos, testes e implementação estejam sempre alinhados.

---

## Agentes disponíveis

### PO — Product Owner

**Arquivo:** `.claude/agents/po.md`

Transforma requisitos brutos em tarefas estruturadas e acionáveis. Recebe uma descrição de necessidade — seja vaga ou técnica — e produz um documento com contexto de negócio, critérios de aceite verificáveis, escopo explícito, estimativa e notas separadas para QA e DEV.

**Quando usar:** sempre que precisar transformar uma ideia ou problema em tarefa de desenvolvimento.

```
/agent:po <descrição do requisito>
```

---

### QA — Quality Assurance

**Arquivo:** `.claude/agents/qa.md`

Recebe a tarefa gerada pelo PO e produz um plano de teste detalhado. Cada critério de aceite vira um ou mais casos de teste numerados com pré-condições, passos e resultado esperado. Inclui cenários negativos, casos de borda, dados de teste necessários e notas de testabilidade para o DEV.

**Quando usar:** após ter a tarefa do PO pronta e antes de iniciar o desenvolvimento.

```
/agent:qa <tarefa gerada pelo PO>
```

---

### DEV — Developer

**Arquivo:** `.claude/agents/dev.md`

Recebe a tarefa do PO e o plano de teste do QA, analisa o repositório e elabora um plano de implementação técnico — arquivos afetados, etapas ordenadas, decisões de design e mapeamento dos casos de teste. **Nenhum código é escrito antes de o usuário aprovar o plano explicitamente.**

**Quando usar:** com a tarefa do PO e o plano do QA em mãos, quando for hora de implementar.

```
/agent:dev <tarefa do PO> + <plano do QA>
```

---

## Fluxo de trabalho

```
Usuário descreve o requisito
        ↓
   /agent:po → Tarefa estruturada
        ↓
   /agent:qa → Plano de teste
        ↓
   /agent:dev → Plano de implementação
        ↓
   Usuário aprova
        ↓
   DEV implementa
```

---

## Estrutura do repositório

```
.claude/
└── agents/
    ├── po.md   # Agente Product Owner
    ├── qa.md   # Agente QA
    └── dev.md  # Agente DEV
```
