# AI-Powered Symfony: From Prototype to Production

A hands-on **Web Summer Camp** workshop on building production-grade AI features with the
Symfony AI components and Anthropic Claude.

> Artificial intelligence is transforming the way we build applications, but integrating LLMs
> into production PHP systems comes with unique challenges. In this workshop you'll build
> AI-powered features using Symfony AI components while tackling real-world concerns such as
> security, cost management, and reliability. You'll create AI agents, implement LLM-powered
> functionality, and defend against prompt-injection attacks — building working features like
> intelligent chatbots, content generation, and automated data processing along the way.

**Duration:** 2.5 hours (with a 30-minute coffee break)
**Audience:** Intermediate Symfony developers — you know controllers, services, and DI. No prior AI/ML experience needed.
**Format:** Balanced theory + hands-on coding.

## What you'll walk away with

- Working code you built during the session
- This repository, with a git tag for every exercise step
- A clear mental model of the LLM integration stack
- Patterns for shipping AI features safely: rate limiting, cost control, prompt-injection defense, and monitoring

## What we'll build

| Module | Topic | You'll build |
|--------|-------|--------------|
| 1 | **LLMs & Symfony AI** | Your first Claude API call in PHP; a token-by-token streaming response |
| 2 | **Building AI features** | A streaming chatbot with session-persisted history; structured output extraction |
| 3 | **AI agents** | A tool-calling agent that runs the ReAct loop — think, act, observe, repeat |
| 4 | **Security** | Defenses against prompt injection: input validation and output classification |
| 5 | **Production** | Rate limiting, token-cost caching, logging, and fallback/retry patterns |

The central idea of Module 3: **an agent is just a PHP loop.** A chatbot answers once; an agent
reasons, calls a tool, observes the result, and repeats until the goal is reached.

## Tech stack

- **PHP** 8.4+
- **Symfony** 8.1
- **Symfony AI** components (`symfony/ai-bundle`) with the Anthropic platform
- **Claude** — `claude-haiku-4-5` for exercises (cheap, fast), `claude-sonnet-4-6` for demos
- **PostgreSQL** 16 (via Docker) for the agent exercise data
- Symfony RateLimiter, Monolog, and the Symfony Profiler for the production module

## Prerequisites

Please have these installed **before** the conference:

1. **PHP 8.4+** on your `PATH`
2. **Composer**
3. **Docker** (for the PostgreSQL database)
4. **Git**
5. **Symfony CLI** — optional but recommended ([install](https://symfony.com/download))

No prior AI/ML knowledge required. An Anthropic API key will be provided on the day — you do
**not** need your own.

## Setup

```bash
# 1. Clone the repo
git clone <this-repo-url> && cd summercamp2026-symfony-ai

# 2. Install PHP dependencies
composer install

# 3. Start the database
docker compose up -d database

# 4. Configure your environment
#    Copy the example and drop in the API key handed out at the session.
cp .env .env.local
#    then edit .env.local and set ANTHROPIC_API_KEY=sk-ant-...

# 5. Run the database migrations
php bin/console doctrine:migrations:migrate

# 6. Start the dev server
symfony serve
#    or, without the Symfony CLI:
php -S localhost:8000 -t public/
```

Then open http://localhost:8000.

## Following along with git tags

Each exercise has a checkpoint you can jump to. To see all of them:

```bash
git tag -l 'step/*'
```

Notable tags include `step/chatbot-skeleton` (Module 2 starting point),
`step/chatbot-complete`, `step/agent-skeleton`, `step/agent-complete`,
`step/secure-chatbot`, and `final` (the complete application). Skeleton tags give you stubs to
fill in; complete tags hold the full solution.

```bash
git checkout step/chatbot-skeleton   # start an exercise
git checkout master                  # back to the latest
```

## Running tests

```bash
php bin/phpunit                       # full suite
php bin/phpunit --filter testName     # a single test
```

---

Built for Web Summer Camp 2026. See [`WORKSHOP.md`](WORKSHOP.md) for the full facilitator
breakdown of modules, timing, and exercises.
