# Configuration Guide

Plain-language explanations of every configurable parameter. Update the "Current value" column with your agent's actual settings from the playground.

| Parameter | What it does (plain language) | Current value |
|---|---|---|
| **Model** | Which AI model powers the agent. Larger models are smarter but slower/costlier. | `gpt-4o` *(update)* |
| **Temperature** | Controls how creative or conservative responses are. Low (0–0.3) = consistent, factual answers. High (0.8+) = more varied, creative phrasing. For a hotel info agent, low is better — guests want accurate answers, not creative ones. | `0.3` *(update)* |
| **Top-p** | Another way to control variety. The model only picks from the most likely words adding up to this probability. Lower = safer, more predictable wording. Usually you adjust temperature *or* top-p, not both. | `1.0` *(update)* |
| **Instructions (system prompt)** | The agent's "job description" — what it knows about the hotel, its tone, and what it should refuse to answer. | *(summarize yours)* |
| **Max tokens** | The maximum length of a response. Keeps answers concise and controls cost. | *(update)* |

## Documentation Checklist

- [ ] All diagrams have alt text
- [ ] Each API endpoint is defined and has an example call
- [ ] Config parameters are listed with short, clear definitions
