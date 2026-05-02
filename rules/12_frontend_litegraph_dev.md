---
name: 12_frontend_litegraph_dev
description: Load this when developing frontend UI elements, LiteGraph widgets, or Vue integrations for custom nodes.
---

# PROTOCOL 12: FRONTEND & LITEGRAPH DEVELOPMENT

## EXTENSION REGISTRATION
- **MANDATE:** When creating custom nodes with UI components, **MUST** register via `app.registerExtension`.
- **RATIONALE:** Ensures your custom Javascript is hooked into the ComfyUI app lifecycle (setup, nodeCreated, beforeRegisterNodeDef).

## WIDGET HANDLING
- **MANDATE:** Do not arbitrarily manipulate the DOM inside the node canvas. Use LiteGraph's built-in widget APIs (`node.addWidget()`).
- **MANDATE:** If a custom widget must be drawn (e.g., a canvas or complex slider), override `node.onDrawForeground` or `node.onDrawBackground` using the Canvas 2D context.

## STATE SYNCHRONIZATION
- **MANDATE:** Ensure UI state is serialized. If your custom JS modifies a node's state, **MUST** update `node.properties` or `node.widgets[i].value` so that the backend receives the correct data during serialization (`workflow.json`).

## VUE INTEGRATION
- ComfyUI's modern frontend utilizes Vue.
- **IF** creating floating dialogs or sidebar panels: Leverage the existing Vue component system where possible rather than injecting raw HTML strings, to maintain the application's aesthetic and state management constraints.

## FRONTEND TESTING
- **UI AUTOMATION:** Utilize community-driven Dockerized ComfyUI environments to run **Playwright-based UI tests** specifically for custom nodes and complex frontend interactions.
- **CROSS-BROWSER:** Ensure extensions are tested against Chromium and Firefox engines within the CI pipeline.
