# Roster

[`roster.yaml`](../skills/blueprint/roster.yaml) sits beside `SKILL.md` and says which models run the recon groups. The skill text never names a model, so you only change this file.

```yaml
code:      # group A, codebase
  - {provider: inherit, model: inherit, effort: inherit, instances: 1}
stack:     # group B, stack and docs
  - {provider: inherit, model: inherit, effort: inherit, instances: 1}
research:  # group C, finders and readers; synthesis uses the first entry
  - {provider: inherit, model: inherit, effort: inherit, instances: 3}
```

## Fields

| Field | Meaning |
|---|---|
| `provider` | An exact provider instance id, from T3 Code's `orchestrator_capabilities` |
| `model` | A model id that provider lists. Naming a provider means naming its model too |
| `effort` | Mapped to that model's own option (`effort`, `reasoningEffort`, ...) |
| `instances` | How many delegates this entry may run at once, per step |

`inherit` (or a missing field) uses your own provider, model, or effort. A missing `instances` means 1.

## How work is spread

1. List the distinct units: one question or angle each.
2. Give one unit per delegate, round-robin across the entries.
3. No two delegates share a unit.
4. Spare instances stay idle. Work is never invented to fill them.
5. More units than instances: related units are bundled.

Before more than 3 delegates start at once, blueprint shows who does what and warns that each one uses account quota.

## Mixing models

A group is a list, so it can mix providers:

```yaml
research:
  - {provider: <provider-a>, model: <model-a>, effort: high, instances: 4}
  - {provider: <provider-b>, model: <model-b>, effort: high, instances: 2}
```

Provider ids are local to a machine, such as a second account of the same provider. If you sync this file across machines, keep the defaults on `inherit`, and name accounts in the request for that run:

```
blueprint, research with <provider-a> x4: ...
```

A role named in the request overrides the roster.

## Council

The council isn't in the roster. The `council` skill picks its own members: one flagship model per provider, three providers.

## Unavailable members

blueprint never substitutes a model.

- An unavailable `research` entry ends group C. The run continues, and blueprint says so.
- Any other unavailable member stops the run, and the plan stays `draft`.
