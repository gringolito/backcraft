---
name: spike
description: >-
  Investigate a spike issue, post the findings on it, and create follow-on items.
  Use once a spike is selected or when the user wants to conduct a spike.
---

Run a spike from its question to findings posted on the spike issue. The deliverable is knowledge:
findings that answer the spike's question and recommend a path, and backlog items for the work
the recommendation implies. The done state is the findings posted as a comment on the spike issue,
the follow-on items created, and the spike issue closed.

Read the spike issue and its comments, and its parent if it has one. Clear up anything unclear
before investigating.

Prototypes are allowed but only to answer the question, and are thrown away. Findings that say
"abandon" or "not feasible" are valid outcomes.

Write the findings as one comment on the spike issue. They restate the question, say what was
investigated and which sources and prototypes were used, report what was learned including dead
ends, give the recommendation, and list the proposed follow-on items. Keep the findings clean,
tight, concise, technical and direct. The findings live on the issue only; nothing is committed
to the repository and no pull request is opened.

Once the findings are posted, ask the user to approve the proposed follow-on items, then create
the approved ones through `add-item`. Each one refers back to the spike and links its findings
comment, and becomes a sub-issue of the spike's parent when it has one. Then close the spike
issue as completed.
