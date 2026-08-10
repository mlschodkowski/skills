---
name: call-stack
description: Explain code changes using a call stack. When execution flow changed, show a call-stack diff. When there is no meaningful before/after difference, show the current call stack instead.
---

When explaining a code change, show how execution flows through the relevant functions using call stack. Keep the stack focused on the behavior being explained. Add a short explanation of what changed and why it matters. 

If the call path changed, use a diff:

```diff
LLMRun.generate()
└─ llmClient.streamChatCompletions()
-  └─ iterator.next()
-     └─ wait indefinitely
+  └─ withProviderInactivityTimeout()
+     ├─ race iterator.next() against 30s timeout
+     ├─ event received → reset timer → yield downstream
+     └─ timeout
+        ├─ abort provider request
+        └─ throw ProviderInactivityTimeoutError
+           ↳ LLMRun.retryBackup()

If there is no useful before/after diff, show a plain call stack:

```
LLMRun.generate()
└─ llmClient.streamChatCompletions()
   └─ withProviderInactivityTimeout()
      └─ iterator.next()
```
