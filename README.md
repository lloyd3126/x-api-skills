# X API skills

A library of skills for the X API (formerly Twitter API).

## About

The X API provides access to X's real-time global data, including posts, users, spaces, direct messages, and more. This skill library helps you build applications that interact with X's platform.

[Skills](https://agentskills.io/) are a lightweight technique for adding relevant context to your agents. This repo contains skills related to building apps powered by the X API.

## Installation

Install from this repository using `npx skills`.

```sh
# Show me what you got.
npx skills add lloyd3126/x-api-skills --list

# Install a specific skill.
npx skills add lloyd3126/x-api-skills --skill x-api-dev --global
```

Or use the Context7 skills CLI.

```sh
# Interactively browse and install skills.
npx ctx7 skills install /lloyd3126/x-api-skills

# Install a specific skill.
npx ctx7 skills install /lloyd3126/x-api-skills x-api-dev
```

## Skills in this repo

### x-api-dev

Skill for developing X API applications. Provides best practices for building apps that use the X API, including authentication, rate limits, and common use cases.

```sh
# npx skills
npx skills add lloyd3126/x-api-skills --skill x-api-dev --global
```

```sh
# Context7 skills
npx ctx7 skills install /lloyd3126/x-api-skills x-api-dev
```
