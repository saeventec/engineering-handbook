# Engineering Handbook

My personal path from junior to senior software engineer, learned step by step with the help of AI.

This repo is a **knowledge base**. Each topic a professional engineer should know is a short, simple lesson with practical examples.
I write it for myself, but anyone is welcome to read and learn from it.

> It won't make anyone senior on its own. Real experience does that.
> The goal is a solid background, so real-world experience makes sense faster.

## How it's organized

| Tier | Folder | What it is |
|---|---|---|
| 1 · Core | `tier-1-core/` | Used almost every day. Learn deeply, in order. |
| 2 · Growth | `tier-2-growth/` | What takes you from junior to mid and senior. |
| 3 · Awareness | `tier-3-awareness/` | Know it exists and when it matters. |

Each tier is split into **areas** (e.g. Python, Databases, Security). Each area is split into **lessons**:

```
tier-1-core/
└── 03-python/
    └── 04-built-in-collections/
        └── README.md        ← the lesson (+ example files if needed)
```

Lesson folders appear as lessons are written. Every lesson follows the same structure: TL;DR, the idea, examples, real-world use, common mistakes, self-check questions, Q&A and sources.

## Key files

| File | Purpose |
|---|---|
| [ROADMAP.md](ROADMAP.md) | The plan: all lessons in learning order |
| [PROGRESS.md](PROGRESS.md) | Where I am: current lesson, where I stopped, counts and a log of every lesson |
| [GLOSSARY.md](GLOSSARY.md) | Short definitions of every term, linked to lessons |
| [TEMPLATE.md](TEMPLATE.md) | The structure every lesson follows |
| [AGENTS.md](AGENTS.md) | Instructions for the AI mentor (works with any AI tool) |
| [CLAUDE.md](CLAUDE.md) | Points Claude to AGENTS.md |
| [mise.toml](mise.toml) | Tool versions for running examples (`mise install`) |

## How I learn with it

Open the repo with any AI assistant that can read and write files, then:

1. **`start`**: the AI writes (or resumes) the next lesson from the roadmap.
2. **Read the lesson and ask questions.** The AI answers, and saves only the useful Q&A in the lesson.
3. **`finish`**: the AI writes key takeaways, updates the progress and commits.

All progress lives in the files, so I can continue on any device, in any session, with any AI.
