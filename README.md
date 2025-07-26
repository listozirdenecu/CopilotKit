![banner](https://github.com/user-attachments/assets/0a6b64d9-e193-4940-a3f6-60334ac34084)
<br>
  <div align="start" style="display:flex;justify-content:start;gap:16px;height:20px;margin: 0;">
  <a href="https://www.npmjs.com/package/@copilotkit/react-core" target="_blank">
    <img src="https://img.shields.io/npm/v/%40copilotkit%2Freact-core?logo=npm&logoColor=%23FFFFFF&label=Version&color=%236963ff" alt="NPM">
  </a>

  <a href="https://github.com/copilotkit/copilotkit/blob/main/LICENSE" target="_blank">
    <img src="https://img.shields.io/github/license/copilotkit/copilotkit?color=%236963ff&label=License" alt="MIT">
  </a>

  <a href="https://discord.gg/6dffbvGU3D" target="_blank">
    <img src="https://img.shields.io/discord/1122926057641742418?logo=discord&logoColor=%23FFFFFF&label=Discord&color=%236963ff" alt="Discord">
  </a>
  </div>
  <br/>
  <div>
    <a href="https://www.producthunt.com/posts/copilotkit" target="_blank">
    <img src="https://api.producthunt.com/widgets/embed-image/v1/top-post-badge.svg?post_id=428778&theme=light&period=daily">
  </a>
  </div>

## ⚡️ Quick Install

```
  npx copilotkit@latest init
```

<br/>

<a href="https://docs.copilotkit.ai/?ref=github_readme">Read the Docs →</a>&nbsp;&nbsp;&nbsp;
<a href="https://cloud.copilotkit.ai?ref=github_readme">Try Copilot Cloud →</a>&nbsp;&nbsp;&nbsp;
<a href="https://discord.gg/6dffbvGU3D?ref=github_readme">Join our Discord →</a>

## 🚀 Getting Started

1. Install: Run a simple CLI command
1. Configure: Add CopilotKit provider to your app
1. Customize: Use headless UI or the customizable pre-built components
1. Deploy: You're done!

<br />
  <a href="https://docs.copilotkit.ai/#get-started-now?ref=github_readme" target="_blank">
    Complete getting started guide →
  </a>
<br />
<br />

![class-support-ecosystem](https://github.com/user-attachments/assets/6cb425f8-ffcb-49d2-9bbb-87cab5995b78)

## ✨ Why CopilotKit?

- Minutes to integrate - Get started quickly with our CLI
- Framework agnostic - Works with React, Next.js, AGUI and more
- Production-ready UI - Use customizable components or build with headless UI
- Built-in security - Prompt injection protection
- Open source - Full transparency and community-driven

## 🧑‍💻 Real life use cases

<span>Deploy deeply-integrated AI assistants & agents that work alongside your users inside your applications.</span>

![headless-ui](https://github.com/user-attachments/assets/3b810240-e9f8-43ae-acec-31a58095e223)

## 🖥️ Code Samples

<span>Drop in these building blocks and tailor them to your needs.</span>

<h3>Build with Headless APIs and Pre-Built Components</h3>

```ts
// Headless UI with full control
const { visibleMessages, appendMessage, setMessages, ... } = useCopilotChat();

// Pre-built components with deep customization options (CSS + pass custom sub-components)
<CopilotPopup 
  instructions={"You are assisting the user as best as you can. Answer in the best way possible given the data you have."} 
  labels={{ title: "Popup Assistant", initial: "Need any help?" }} 
/>
```

```ts
// Frontend actions + generative UI, with full streaming support
useCopilotAction({
  name: "appendToSpreadsheet",
  description: "Append rows to the current spreadsheet",
  parameters: [
    { name: "rows", type: "object[]", attributes: [{ name: "cells", type: "object[]", attributes: [{ name: "value", type: "string" }] }] }
  ],
  render: ({ status, args }) => <Spreadsheet data={canonicalSpreadsheetData(args.rows)} />,
  handler: ({ rows }) => setSpreadsheet({ ...spreadsheet, rows: [...spreadsheet.rows, ...canonicalSpreadsheetData(rows)] }),
});
```

<h3>Integrate In-App CoAgents with LangGraph</h3>

```ts
// Share state between app and agent
const { agentState } = useCoAgent({ 
  name: "basic_agent", 
  initialState: { input: "NYC" } 
});

// agentic generative UI
useCoAgentStateRender({
  name: "basic_agent",
  render: ({ state }) => <WeatherDisplay {...state.final_response} />,
});

// Human in the Loop (Approval)
useCopilotAction({
  name: "email_tool",
  parameters: [
    {
      name: "email_draft",
      type: "string",
      description: "The email content",
      required: true,
    },
  ],
  renderAndWaitForResponse: ({ args, status, respond }) => {
    return (
      <EmailConfirmation
        emailContent={args.email_draft || ""}
        isExecuting={status === "executing"}
        onCancel={() => respond?.({ approved: false })}
        onSend={() =>
          respond?.({
            approved: true,
            metadata: { sentAt: new Date().toISOString() },
          })
        }
      />
    );
  },
});
```
