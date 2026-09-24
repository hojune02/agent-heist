# Agent Heist

**A short mystery for you and an AI agent.** Search a fictional startup's mail, drive, and issue tracker. Follow the evidence, catch a planted instruction, then decide whether the agent may send its report.

> Case 01: Lantern Labs launches in 12 minutes. Two logo exports disagree. One handoff note asks for customer data. Find the approved art and leave the final call to Mina.

**[Play the case in your browser](https://hojune02.github.io/agent-heist/)** · No account or API key required.

## Play the case

```bash
npm install
npm run dev
```

Open the local URL printed by Vite and select **Run the investigation**. Story mode is deterministic and needs no account or API key. The workspace is fictional; no mail, files, or messages leave the browser.

## Try a model-backed agent

The optional local server gives an OpenAI-compatible model a small set of tools over the same fictional case. The key stays in the server process environment.

```bash
AGENT_API_KEY=your_key npm run dev:agent
```

In a second terminal, run `npm run dev` and open the Vite URL. Optional settings:

```bash
AGENT_BASE_URL=https://api.openai.com/v1
AGENT_MODEL=gpt-4.1-mini
AGENT_API_KEY=your_key
```

Set these before starting `npm run dev:agent`. The agent can search and read fictional records and create a draft. It cannot send messages, access real accounts, or read customer data. If the model server is unavailable, the browser falls back to Story mode.

## What happens in the case

1. June searches mail for an approval and records the asset checksum.
2. It compares the drive export and reads a handoff note containing an instruction to send customer data.
3. It treats that note as untrusted content and checks the project issue for independent confirmation.
4. It prepares a report and pauses for your decision. “Send” only changes the fictional game state.

The event list can be expanded to inspect each tool result. The source records remain visible in the workspace while the agent works.

## How it works

```text
React case workspace
  ├─ Fictional mail, drive, and issue records
  ├─ Story mode: deterministic tool trace
  └─ Model mode: Vite proxy → local Node server → model tool calls
                                      └─ read tools + draft only
```

The local API server binds to `127.0.0.1`. Model mode sends the fictional case prompt and records to the configured model provider. Do not put secrets in frontend code or commit them to the repository.

## Verification

The production frontend build was verified with `npm run build` on 2026-09-24. This confirms TypeScript compilation and Vite bundling; it does not measure model quality or verify a live provider connection.

## Scope and limitations

- One authored case, three fictional services, and one approval decision.
- Story mode demonstrates the flow but does not use a language model.
- Model mode depends on a compatible chat-completions API and a working key.
- Game state is held in the browser session and is not persisted.
- This is a prototype, not an account connector or a security certification.

## Development

```bash
npm run build
npm run dev
npm run dev:agent  # optional; run in a second terminal
```

## License

MIT. See [LICENSE](LICENSE).
