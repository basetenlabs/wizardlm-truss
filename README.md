# WizardLM Truss

This repository packages [WizardLM](https://github.com/nlpxucan/WizardLM) as a [Truss](https://truss.baseten.co).

WizardLM is a instruction-following LLM tuned using the Evol-Instruct method. Evol-Instruct is a novel method using LLMs instead of humans to automatically mass-produce open-domain instructions of various difficulty levels and skills range, to improve the performance of LLMs.

Utilizing this model for inference can be challenging given the hardware requirements. With Baseten and Truss, inference is dead simple.

## Deploying WizardLM

To deploy, make sure you have a Baseten account and API key. You can sign up for a Baseten account [here](https://app.baseten.co/signup).

**Setup:**

```
pip install --upgrade baseten
baseten login
```

**Deployment**

```
git clone git@github.com:basetenlabs/wizardlm-truss.git
cd wizardlm-truss
truss push --model-name="WizardLM" --remote-name="baseten"
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
model.predict({"prompt": "What is the difference between a wizard and a sorcerer?"})
```

You can also invoke your model via a REST API

```
curl -X POST " https://app.baseten.co/models/YOUR_MODEL_ID/predict" \
     -H "Content-Type: application/json" \
     -H 'Authorization: Api-Key {YOUR_API_KEY}' \
     -d '{
           "prompt": "What is the difference between a wizard and a sorcerer?",
           "temperature": 0.3
         }'
```

## Hardware

We found this model runs reasonably fast on A10Gs; you can configure the hardware you'd like in the `config.yaml`.

Default config:

```yaml
...
resources:
  cpu: "3"
  memory: 14Gi
  use_gpu: true
  accelerator: A10G
...
```