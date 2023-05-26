# WizardLM Truss

This repository packages [WizardLM](https://github.com/nlpxucan/WizardLM) as a [Truss](https://truss.baseten.co).

## Deploying WizardLM

WizardLM is a instruction-following LLM tuned using the Evol-Instruct method. Evol-Instruct is a novel method using LLMs instead of humans to automatically mass-produce open-domain instructions of various difficulty levels and skills range, to improve the performance of LLMs.

Utilizing this model for inference can be challenging given the hardware requirements. With Baseten and Truss, this can be dead simple. You can see the full code repository here.

We found this model runs reasonably fast on A10Gs; you can configure the hardware you'd like in the `config.yaml`.

```yaml
...
resources:
  cpu: "3"
  memory: 14Gi
  use_gpu: true
  accelerator: A10G
...
```

Deploying the Truss is easy; simply load it and push.

```python
import baseten
import truss

wizardlm_truss = truss.load('.')
baseten.deploy(wizardlm_truss)
```

## Invoking WizardLM

The usual GPT-style parameters will pass right through to the inference point:

* max_new_tokens (_default_: 64)
* temperature (_default_: 0.5)
* top_p (_default_: 0.9)
* top_k (_default_: 0)
* num_beams (_default_: 4)


```python
import baseten
model = baseten.deployed_model_id('YOUR MODEL ID')
model.predict({"prompt": "What's the weather like?"})
```
