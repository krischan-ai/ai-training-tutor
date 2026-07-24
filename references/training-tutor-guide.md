# AI Training Tutor Guide

## Generic beginner training path

Use this order unless the repository clearly defines a different one:

1. Understand the task boundary and data source.
2. Prepare the environment and confirm the right Python/interpreter is active.
3. Confirm GPU/accelerator availability if training needs it.
4. Configure model and dataset caches deliberately.
5. Start monitoring before training.
6. Validate datasets and splits.
7. Run a dry-run, config preview, or plan generation step.
8. Run a tiny smoke experiment.
9. Evaluate the smoke output.
10. Scale to the intended model/data size.
11. Evaluate again and inspect generated examples.
12. Record configuration, data version, metrics, logs, failures, and conclusions.

## Concepts to explain for novices

| Concept | Beginner explanation |
| --- | --- |
| Dataset split | Separate training, validation, and test data so evaluation is not just memorization |
| Gold sample | Human-reviewed, traceable, accepted data that can be trusted for training or evaluation |
| Synthetic data | Generated or simulated data useful for engineering tests but not automatically production evidence |
| Dry-run | A safe preview that checks config and writes a plan without doing expensive training |
| Smoke run | A tiny run to verify the pipeline before spending time and GPU resources |
| Epoch | One pass through the training set |
| Loss | A training signal showing how well the model predicts the target text, not direct business quality |
| Validation loss | Loss on held-out validation data, useful for overfitting checks |
| Gradient norm | A rough stability signal for the training update size |
| Checkpoint | Saved training state or model/adapter snapshot |
| Adapter | Small trained weights attached to a base model, common in LoRA-style fine-tuning |
| Quantization | Loading weights in lower precision to reduce memory use |
| Preference pair | Two answers for the same prompt, one preferred and one rejected |

## Monitoring guidance

Monitoring is not decoration. Explain it as the learner's dashboard for answering:

- Is training still running?
- Is loss decreasing smoothly or exploding?
- Did evaluation run at the expected time?
- Which config produced this result?
- Where are artifacts and checkpoints stored?

Common tools:

- MLflow: experiment registry, run comparison, parameters, metrics, artifacts.
- TensorBoard: training curves and event logs.

If either tool fails, training can often still run, but the learner loses observability. Teach the user to fix monitoring early when the goal is learning.

## Dataset acceptance standards

Before formal training or serious evaluation, require:

- Known data source and license.
- No unintended sensitive personal information.
- Stable schema with required fields present.
- Valid labels or outputs.
- Train/validation/test split without leakage.
- Duplicate and near-duplicate checks where relevant.
- Human review process for gold data.
- Frozen test set for fair comparison.
- A manifest or report recording source, version, count, checksums, and limitations.

For classroom or engineering experiments, allow synthetic data only if the limitation is stated clearly.

## Experiment acceptance standards

A successful training command alone is not enough. Require:

- Config and output directory recorded.
- Data version recorded.
- Monitoring logs or equivalent training logs available.
- Checkpoint or adapter saved if expected.
- Evaluation run on a held-out split.
- Metrics interpreted in task terms.
- Several predictions manually inspected.
- Known limitations written down.

## Common troubleshooting categories

### Environment and dependency

Symptoms include missing modules, wrong Python path, package version conflicts, or commands from the wrong virtual environment. First check `which python`, package version, and whether the virtual environment is active.

### Permission and ownership

Symptoms include `Permission denied` during cache writes, pip installs, checkpoint saves, or database writes. Common cause: mixing root/admin and normal-user commands. Teach ownership inspection before broad permission fixes.

### Port already in use

Monitoring or serving tools often fail when a port is already occupied. Teach checking the listener and either stopping the old process intentionally or choosing a different port.

### Model download and cache

Symptoms include timeouts, SSL failures, lock-file permission errors, or repeated downloads. Explain that different model sources, model sizes, revisions, and cache roots do not automatically share files.

### GPU memory

Symptoms include out-of-memory errors or process termination. Prefer reducing batch size, sequence length, or using quantized/adapter training before changing model architecture.

### Training quality

Low training loss can still produce poor task metrics. Ask for evaluation output and generated predictions. Separate format errors, label errors, truncation, hallucination, and true reasoning failures.

### Evaluation quality

If metrics look wrong, inspect prediction files and label normalization before assuming the model is bad. Confirm output schema, max generation length, split, and metric definitions.

## Response style

Prefer concise, stepwise Chinese when the user is Chinese. Give one or two concrete next actions for active troubleshooting. For document writing, use a patient tutorial tone: purpose first, operation second, interpretation third.
