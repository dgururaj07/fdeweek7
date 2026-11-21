# OpenAI GPT-6.2 Models (Astra & Sol)

*Released November 17, 2026. Notes compiled November 22, 2026.*

## Overview

GPT-6.2 is a family of **two models**:

- **GPT-6.2 Astra** is OpenAI's new frontier model, built for the hardest, most complex projects.
- **GPT-6.2 Sol** is the efficient, lower-cost model for everyday work. OpenAI says it gets close to Astra on coding at about one-fifth of the price.

## Model Specifications

| Spec | GPT-6.2 Astra | GPT-6.2 Sol |
|------|---------------|-------------|
| **API model ID** | `gpt-6.2-astra` | `gpt-6.2-sol` |
| **Positioning** | Frontier / flagship | Everyday / cost-efficient |
| **Context window** | ~1.05M tokens * | ~1.05M tokens * |
| **Max output** | 128K tokens * | 128K tokens * |
| **Input price** (per 1M tokens) | $8.00 | $2.00 |
| **Cached input** (per 1M tokens) | $0.40 | $0.10 |
| **Output price** (per 1M tokens) | $40.00 | $10.00 |
| **Price change** | 20% cheaper than GPT-6 Astra | Same price as GPT-6.1 Sol |

\* *From third-party reporting. OpenAI's announcement and API guide don't state the context window or max output. Check the [OpenAI model docs](https://developers.openai.com/api/docs/guides/latest-model) before relying on these figures. One outlet reported a 1.1M-token context window, which conflicts with the rest.*

## Availability

- **API:** both models are available through the OpenAI API.
- **ChatGPT Work and Codex:** rolling out to Plus, Pro, Enterprise and Edu users.
- **Not in regular ChatGPT Chat:** this release does not add either model to standard Chat.

## Performance Highlights

- OpenAI reports that **Astra** leads its tested models on professional-output evaluations.
- **Sol** gets close to Astra on coding tasks at roughly 1/5 the cost.
- A third-party arena ranking put Astra first (~1,318 Elo), ahead of Claude Fable 5.2 (~1,271) and GPT-6.2 Sol (~1,259). Leaderboard positions change often.

## Safety

- According to the system card, **Astra** is the first OpenAI model rated **"High" for AI Self-Improvement** under OpenAI's Preparedness Framework. Sol is rated below that threshold.
- Both models meet the **"Critical" threshold for cybersecurity** and the **"High" threshold for bio/chem**. OpenAI launched them with **tighter safeguards** for higher-risk cybersecurity requests. These may block some legitimate security research.

## What's New in GPT-6.2

### Capabilities (vs GPT-6 / GPT-6.1)
- **Professional output:** better slides, spreadsheets and documents that follow templates and field conventions. Astra can match a template from a screenshot.
- **Coding:** cleaner code, more focused tests on existing codebases and fewer revision rounds. Stronger frontend and 3D / interactive web work.
- **Computer use:** more precise, down to individual parts in CAD and simulation tools.
- **Agents and tool use:** better judgment about how much effort a task needs and when to use plugins versus computer use. Sol handles multistep agentic workflows well.
- **Token efficiency:** Astra used 22% fewer output tokens than GPT-6 Astra on GDPval v2 while scoring 6.2 points higher. Astra is also more concise by default.

### Pricing and access
- Astra is **20% cheaper** than GPT-6 Astra on input and output, with a **60% discount on cached input**. Sol keeps GPT-6.1 Sol's prices.
- **Ultrafast** processing is available for both models in the API at launch (US data residency only).
- Both models support US and EU data residency with Standard, Fast and Batch processing. **Flex processing is not supported.** **Background mode** (public beta) offers 2-hour or 8-hour completion windows.

### Key benchmark gains (OpenAI's own figures)
| Benchmark | Result |
|-----------|--------|
| Agents' Last Exam | Astra scores +5.2 points vs GPT-6 Astra at under 1/3 the cost |
| Terminal-Bench-Science 0.1 | Astra scores +9 points vs GPT-6 Astra |
| FrontierCode 2.0 | Sol scores within 0.5 points of Astra at about 1/5 the cost |
| LifeVal | Sol beats GPT-6 Astra at about 1/7 the cost |
| GDPval v2 | Astra scores +6.2 points vs GPT-6 Astra; Sol scores +5.3 points vs GPT-6.1 Sol |
| Harvey LAB-AA v1.1 | Astra sets a new state of the art |

### API changes developers must handle
- **Sampling parameters removed:** `temperature`, `top_p`, `logprobs` and `top_logprobs` are not supported.
- **Tool calling requires the Responses API.** Chat Completions still works, but not for tools.
- **`instructions` placement:** top-level `instructions` is now appended *after* `input`. For caching, put stable instructions in a `developer` message as the first input item.
- **Reasoning effort:** start new integrations at `medium`. Replace `none` or `minimal` with `low`.
- **Prompt caching:** replace `prompt_cache_retention` with `prompt_cache_options.ttl` (for example `"30m"`).
- **Prefix edits:** editing the conversation history mid-conversation, switching models, or changing the user or org drops reasoning items. This can lower answer quality and raise token use.

## FDE Takeaways

- **Model choice:** default to **Sol** for most customer workloads (chat, RAG, coding help). Move up to **Astra** only for the hardest reasoning or agentic tasks where the extra cost (4x Sol) is worth it.
- **Large context:** ~1M tokens means whole codebases or large document sets fit in one prompt. Still track token cost (see LLM observability tools in [observability-tools.md](observability-tools.md)).
- **Cost control:** use cached input pricing for repeated system prompts and shared context.
- **Access check:** confirm the customer's plan and region have API access before promising a GPT-6.2 deployment.

## Sources

- [Introducing GPT-6.2 Astra and Sol (OpenAI)](https://openai.com/index/introducing-gpt-6-2-astra-sol/)
- [Using GPT-6.2 (OpenAI API docs)](https://developers.openai.com/api/docs/guides/latest-model)
- [GPT-6.2 System Card (OpenAI Deployment Safety Hub)](https://deploymentsafety.openai.com/gpt-6-2-astra-sol)
- [GPT-6.2 Astra and Sol are now available (OpenAI Developer Community)](https://community.openai.com/t/gpt-6-2-astra-and-sol-are-now-available/1417531)
- [MarkTechPost: OpenAI Releases GPT-6.2 Astra and Sol](https://www.marktechpost.com/2026/11/17/openai-gpt-6-2-astra-sol-release/)
- [Data Studios: GPT-6.2 Astra and Sol pricing and access](https://www.datastudios.org/post/openai-gpt-6-2-astra-sol-launch-api-pricing-chatgpt-codex)
- [eesel.ai: GPT-6.2 Astra overview](https://www.eesel.ai/blog/gpt-6-2-astra)
