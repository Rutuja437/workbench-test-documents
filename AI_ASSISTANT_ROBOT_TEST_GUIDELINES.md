# Agentic Instructions for CampusTrack AI Assistant UI

## Purpose

Provide high-level instructions to an AI agent so it can understand the UI structure and automatically generate reusable Robot Framework tests. The agent should rely on standard component identifiers instead of fragile XPath or DOM-position-based locators.

---

# 1. AI Assistant Panel

## Identification Rules

- Locate the AI Assistant panel using `data-testid="ai-assistant-panel"` or a custom component such as `<ct-ai-panel>`.
- The panel should have a unique identifier independent of its DOM position.
- Identify the panel header, conversation area, suggested prompts, input field, and send button as child components.

## Agent Instructions

```text
Locate the AI Assistant panel.

Verify the panel is visible.

Identify all child components within the panel.

Generate Robot Framework tests to verify:
- The panel opens successfully.
- The panel closes successfully.
- The panel remains accessible while navigating the application.
- The panel layout remains consistent.
- The panel does not overlap or hide critical dashboard functionality.

Report any component that cannot be uniquely identified.
```

---

# 2. Conversation Area

## Identification Rules

- Locate the conversation container using `data-testid="chat-conversation"`.
- Identify user messages and assistant messages using separate identifiers.
- Each message should have a unique message container.

## Agent Instructions

```text
Locate the conversation area.

Identify user messages and assistant responses.

Generate Robot Framework tests to verify:
- Messages appear in chronological order.
- User and assistant messages are visually distinguishable.
- New responses appear after prompt submission.
- Conversation history remains visible.

Report inconsistencies in message rendering.
```

---

# 3. Suggested Prompt Chips

## Identification Rules

- Locate the prompt suggestion container.
- Identify every suggested prompt using a reusable identifier such as `data-testid="suggestion-chip"`.

## Agent Instructions

```text
Locate all suggested prompt chips.

Generate Robot Framework tests to verify:
- Every suggestion is visible.
- Every suggestion is clickable.
- Selecting a suggestion triggers the expected prompt.
- Suggestions remain accessible after previous interactions.

Report prompt chips without unique identifiers.
```

---

# 4. Chat Input

## Identification Rules

- Locate the chat input using `data-testid="chat-input"`.
- Associate the send button with the input field.

## Agent Instructions

```text
Locate the chat input.

Generate Robot Framework tests to verify:
- The input field accepts user input.
- The input field supports editing.
- Empty prompts are handled appropriately.
- Prompt submission triggers an AI response.

Report missing identifiers.
```

---

# 5. Send Button

## Identification Rules

- Locate the send button using `data-testid="send-button"`.

## Agent Instructions

```text
Locate the send button.

Generate Robot Framework tests to verify:
- The button is visible.
- The button is enabled when input is provided.
- Clicking the button submits the prompt.
- The corresponding response is displayed.

Report button identification issues.
```

---

# 6. Dashboard Tabs

## Identification Rules

- Locate the tab container using `data-testid="tab-container"`.
- Identify each tab using `data-testid="tab"`.

## Agent Instructions

```text
Locate all dashboard tabs.

Generate Robot Framework tests to verify:
- Every tab is visible.
- Every tab is selectable.
- Switching tabs updates the displayed content.
- Only one tab remains active at a time.

Report tabs without reusable identifiers.
```

---

# 7. Dashboard Data Table

## Identification Rules

- Locate the table using `data-testid="data-table"`.
- Identify headers, rows, and row actions using reusable identifiers.

## Agent Instructions

```text
Locate the dashboard table.

Generate Robot Framework tests to verify:
- Table is displayed correctly.
- Headers are present.
- Rows are rendered correctly.
- Row actions are available.
- Data refreshes correctly after navigation.

Report table elements without identifiers.
```

---

# 8. Left Navigation Sidebar

## Identification Rules

- Locate the application sidebar using `data-testid="sidebar"`.
- Identify every module using `data-testid="sidebar-item"`.

## Agent Instructions

```text
Locate the application sidebar.

Discover all navigation items.

Generate Robot Framework tests to verify:
- Sidebar is visible.
- Navigation items are clickable.
- Selecting a module loads the correct page.
- The selected module is highlighted.

Report navigation items without unique identifiers.
```

---

# 9. Overall Layout

## Identification Rules

- Treat the AI Assistant panel and dashboard as separate reusable components.
- Both components should expose unique identifiers.

## Agent Instructions

```text
Locate the AI Assistant panel and the dashboard.

Generate Robot Framework tests to verify:
- Both components remain visible during interaction.
- Dashboard content is not obscured by the AI Assistant.
- Layout remains responsive across supported screen sizes.
- User can continue interacting with the dashboard while the AI Assistant is open.

Report layout issues and recommend reusable component identifiers where required.
```

---

# General Agent Guidelines

```text
- Prefer data-testid, ARIA labels, roles, or custom HTML components for locating UI elements.
- Avoid XPath based on DOM hierarchy or element position.
- Generate reusable Robot Framework keywords instead of page-specific automation.
- Report components that cannot be uniquely identified as design improvements.
- Follow consistent component identification across all CampusTrack modules to maximize test reusability.
```
