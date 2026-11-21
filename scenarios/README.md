# scenarios

The test set. Each scenario is a reproducible incident with a known root cause and lives in its own folder:

```
scenarios/<id>-<name>/
├── inject      # breaks the cluster in a defined way
├── ground_truth.yaml   # expected triage, root cause and remediation
└── cleanup     # restores the previous state
```

Scenarios are independent of the agent and of the eval harness, so either can be replaced without touching the test set.
