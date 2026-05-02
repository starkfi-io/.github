# StarkFi AI Integration

<p align="center">
  <strong>Connect AI Agents to the StarkFi Ecosystem</strong><br>
  Payments · Yield · Orders · KYC · Smart Contracts
</p>

<p align="center">
  <a href="[https://www.npmjs.com/package/starkfi-mcp](https://www.npmjs.com/package/starkfi-mcp)"><img src="[https://img.shields.io/npm/v/starkfi-mcp?label=npm&logo=npm](https://img.shields.io/npm/v/starkfi-mcp?label=npm&logo=npm)" alt="npm version"></a>
  <img src="[https://img.shields.io/badge/license-MIT-blue.svg](https://img.shields.io/badge/license-MIT-blue.svg)" alt="License MIT">
  <a href="[https://starkfi.mintlify.app/](https://starkfi.mintlify.app/)"><img src="[https://img.shields.io/badge/docs-StarkFi-0A0A0A?logo=readthedocs&logoColor=white](https://img.shields.io/badge/docs-StarkFi-0A0A0A?logo=readthedocs&logoColor=white)" alt="StarkFi docs"></a>
</p>

---

## Overview

Este ecossistema permite que assistentes de IA (Cursor, Claude, LangChain, OpenAI Agents) interajam diretamente com a **[StarkFi](https://starkfi.mintlify.app/)**. Em vez de chamadas REST manuais, sua IA utiliza ferramentas tipadas para gerenciar pagamentos, rendimentos (yield), ordens e KYC.

---

## Integration Methods

Agora você tem duas formas principais de integrar a StarkFi ao seu agente de IA, dependendo da sua arquitetura:

### 1. Model Context Protocol (MCP)
**Melhor para: Usuários de Desktop (Claude Desktop, Cursor, IDEs).**
O servidor MCP expõe a API da StarkFi como ferramentas locais via protocolo `stdio`. É a forma mais rápida de dar "superpoderes" financeiros ao seu editor de código ou chat de desktop.
* **Repo:** [`starkfi-mcp-agent`]([https://github.com/starkfi-io/starkfi-mcp-agent](https://github.com/starkfi-io/starkfi-mcp-agent))
* **Uso:** Configuração via JSON no Claude/Cursor.

### 2. AI Agent Skills (Functional Tools)
**Melhor para: Desenvolvedores construindo Agentes Autônomos (LangChain, AutoGPT, Frameworks customizados).**
Uma biblioteca de funções modulares (skills) que podem ser importadas e injetadas diretamente em qualquer framework de agentes que suporte chamadas de ferramentas (tool calling).
* **Repo:** [`starkfi-agent-skills`]([https://github.com/starkfi-io/starkfi-agent-skills](https://github.com/starkfi-io/starkfi-agent-skills))
* **Uso:** Importe como um módulo e passe para o array de ferramentas do seu LLM.

---

## Features

- **Yield** — Estratégias, oportunidades de rebalanceamento, ganhos e execução de depósitos/saques.
- **Orders** — Listagem, criação, atualização parcial e controle de estado de ordens de pagamento.
- **StarkPay** — Status de pagamentos, registro de intents, criação de transações e tokenização.
- **KYC** — Fluxo completo: envio de OTP, verificação, sessões Didit e consulta de status.

---

## Configuration

Ambos os métodos utilizam as mesmas credenciais básicas:

| Variável | Obrigatório | Descrição |
|----------|:--------:|-------------|
| `STARKFI_API_KEY` | **Sim** | Sua chave de API obtida no [Dashboard StarkFi](https://starkfi.io/) |
| `STARKFI_BASE_URL` | Não | Padrão: `https://api.starkfi.io` |

---

## Quick Start (MCP Server)

Se você deseja usar no **Claude Desktop** ou **Cursor**:

```json
{
  "mcpServers": {
    "starkfi": {
      "command": "npx",
      "args": ["-y", "starkfi-mcp"],
      "env": {
        "STARKFI_API_KEY": "sua_chave_aqui"
      }
    }
  }
}
```

## Quick Start (Skills Library)

Se você está **desenvolvendo um agente** via código:

```bash
npm install @starkfi/agent-skills
```

```typescript
import { getStarkFiSkills } from "@starkfi/agent-skills";

// Injetando as ferramentas no seu agente
const tools = getStarkFiSkills({ apiKey: process.env.STARKFI_API_KEY });
```

---

## Tool Catalog

| Prefixo | Domínio | Descrição |
|--------|--------|-----------|
| `yield_*` | Yield | Estratégias, rebalance, earnings, deposit/withdraw. |
| `order_*` | Orders | Templates de ordens de pagamento: list, create, patch. |
| `starkpay_*` | StarkPay | Lifecycle de pagamento, intents, broadcast on-chain. |
| `kyc_*` | KYC | Fluxo de identidade: prepare, OTP, verify, session. |

---

## Security

> **Atenção:** Nunca exponha sua `STARKFI_API_KEY` em repositórios públicos. Use variáveis de ambiente ou gerenciadores de segredos (Secret Managers). O protocolo MCP opera localmente, garantindo que suas chaves não saiam do seu ambiente controlado.

---

## References

| Recurso | URL |
|----------|-----|
| StarkFi Documentation | [starkfi.mintlify.app](https://starkfi.mintlify.app/) |
| MCP Specification | [modelcontextprotocol.io](https://modelcontextprotocol.io/) |
| StarkFi Dashboard | [starkfi.io](https://starkfi.io/) |

---

## License

[MIT](LICENSE)
