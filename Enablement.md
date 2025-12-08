# Enablement :: Qodo Proof-of-Value

## Topics

* Why a code-review agent in needed.

* How Qodo fits into your development workflow.

* Qodo's internal architecture.

* Configuring Qodo for your needs.

* Enforcing compliance rules.

* Suggesting best practices.

* Model control.

* Additional context & extra instructions.

## Why a code-review agent in needed

* "Too much code"

* "Non-precise implementations"

* "Security and compliance risk"

### "Too much code"

* Generative Ai started off an "auto complete on steroids"

* Vibe coding took Ai code generationb to another level

* Autonomous agents implementing issues, fixing bugs, updating dependencies & writing code.

Everyone is now an engineering-manager with multiple agentic junior devs at their disposal.

Thus, the review bottleneck.

### "Non-precise implementation"

* Ai does things fast, but inaccurate

* Inaccuracies over longer sessions: Agent "forgets" or dilutes the original prompt

* Agent does "too much": While missing things you specifically asked for

* Agent uses the wrong tech (libraries / services / dependencies etc.)

Hard and soft rules enforcement.

### "Security and compliance risk"

* Too much code is created, sometimes inaccurate

* Human attention span is limited

* Security & compliance failures can be disastrous

Hard rules enforcement.

## How Qodo fits into your development workflow

* Enforced standardized reviews via Git

* Local reviews on the developer machine

* Automated reviews via CICD, MCPs, Webhooks, APIs etc.

### Enforced standardized reviews via Git

* Qodo listens to webhooks from your Git platform

* Qodo responds to PR creates & updates

* Configure-able:
  * Tools to execute
  * Rules to enforce
  * Best practices to suggest

### Local reviews on the developer machine

* Developer downloads an Qodo IDE plugin
  * Available for VS Code, Visual Studio, JetBrains IDEs (IntelliJ, PyCharm, WebStorm etc.)

* Developer activates local reviewer in their dev-workflow

-or-

* Developer downloads Qodo CLI
  * `npm install -g @qodo/command`

* Developer activates local reviewer in their dev-workflow

### Automated reviews via CICD, MCPs, Webhooks, APIs etc

* DevOps configures Qodo CLI in their automation suite

* Qodo CLI triggers Audit agents, Documentation agents, Threat Modeling agents etc.

## Qodo's internal architecture

* Tools
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/tools/tools-list>

* Triggers
  * Automatic, upon PR create or PR update events
  * Manual, when the user comments

* Default tools

```toml
# [github_app]
# [gitlab]
[bitbucket_app]
pr_commands = [
    "/describe",
    "/compliance",
    "/improve",
]
```

* Most used

  * `/describe` - Generate PR titles, descriptions, diagrams, file-walkthroughs
  * `/compliance` - Security, Acceptance Criteria, Rules
  * `/improve` - Code suggestions and improvements
  * `/custom_prompt` - Like `/improve` but offers code suggestions based on a custom prompt
  
* Others
  * `/ask` - Free-style Q&A
  * `/help_docs` - Free-style Q&A, answers from the repo's docs folder
  * `/analyze` - Identify components for generating tests, docs and improvements
  * `/create-ticket` - Generates issues for PR in Jira, Linear. GitHub or GitLab
  * `/similar_code` - Retrieves similar / duplicate code

## Configuring Qodo for your needs

* What can be configured.
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/what-can-you-configure>

* Project-specific configuration
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/configuration-file#local-configuration-file>

* Global configuraton
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/configuration-file#global-configuration-file>

## Enforcing compliance rules

* Setting up compliance rules
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/features/custom-compliance>

* Local compliance
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/features/custom-compliance#local-compliance-checklists>

* Global compliance
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/features/custom-compliance#global-hierarchical-compliance>

## Suggesting best practices

* Auto best practices with GitHub

* User defined best practices

### Auto best practices with GitHub

* Scan repo discussions
  * Learn from discussions on historical PRs and generate best practices file
  * `/scan_repo_discussions`
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/tools/tools-list/scan-repo-discussions>

* Auto best practices
  * Keeps track of review suggestions accepted by humans
  * Reinforces and regenerates best practices based on user-acceptance
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/features/best-practices>

### User defined best practices

* Local best practices

* Global hierarchical best practices

* <https://docs.qodo.ai/qodo-documentation/qodo-merge/features/best-practices#auto-best-practices-vs-custom-best-practices>

## Model control

```toml
[config]
model = "gemini-2.5-pro"
fallback_models = ["gpt-5", "claude-4-sonnet"]
```

## Additional context & extra instructions

* Supported files
  * `agents.md`, `qodo.md`, `claude.md`
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/configuration-file/additional-context#supported-file-formats>

* Custom files
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/configuration-file/additional-context#supported-file-formats>

* Extra instructions
  * All tools accept an `extra_instructions` parameter that allows you to add free-text extra instructions.
  * <https://docs.qodo.ai/qodo-documentation/qodo-merge/configuration/configuration-file/configuration-options#extra-instructions>

* Language settings
  * All tools accept an extra_instructions parameter that allows you to add free-text extra instructions.

    ```toml
    [config]
    response_language = "de-DE"
    ```

* Ignoring files

    ```toml
    [ignore]
    glob = ['*.py']
    regex = ['.*\.py$']
    ```

* Ignore PRs

```toml
[config]
ignore_pr_title = ["\\[Bump\\]"]
ignore_pr_source_branches = ['develop', 'main']
ignore_pr_target_branches = ["qa"]
ignore_pr_labels = ["do-not-merge"]
ignore_pr_authors = ["my-special-bot-user"]

allow_only_specific_folders = ['folder1', 'folder2']  # reviews only when specific folders are modified
```
