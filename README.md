AGENTS.md and SOUL.md setup for Hermes Agent.

```
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

```
npm install -g @anthropic-ai/claude-code
```

```
claude auth login
```

```
cp SOUL.md config.yaml ~/.hermes/
```

```
hermes plugins install claude-subscription-directsdk
```

```
hermes skills install JuliusBrussee/caveman/skills/caveman --force
```

```
git clone https://github.com/DietrichGebert/ponytail.git ~/.hermes/plugins/ponytail
hermes plugins enable ponytail
```

Other helpfull tools:
- https://github.com/alexgreensh/token-optimizer
- https://github.com/tirth8205/code-review-graph
- https://github.com/rtk-ai/rtk
