## **Dataset**

https://www.kaggle.com/datasets/archanghosh/robert-frost-collection/code

Small dataset with only 107 poems.

---

**Dataset Pre-processing**

- Each poem was formatted using explicit poem boundary tokens: <|startofpoem|> + poem content + <|endofpoem|>
- Dataset was split into 90% training and 10% testing

---

## **Models**

### GPT-2 Small: Transformer Layers = 12
Experimented with:
- Full Fine-Tuning (all layers trainable)
- Partial Fine-Tuning (only last 2 layers trainable)


### GPT-2 Medium: Transformer Layers = 24
Experimented with:
- Partial Fine-Tuning (only last 4 layers trainable)

---

**Training Configuration**

|Parameter|Value|
|---------|-----|
|Learning Rate	|5e-5|
|Epochs|	10|
|Weight Decay|	0.01|
|FP16 Training|	Enabled|
|Gradient Accumulation|	8|
|Evaluation Strategy|	Every Epoch|
|Save Strategy|	Every Epoch|

---

**Results**

1. GPT-2 Small (Full Fine-Tuning)

|Metric|	Value|
|------|---------|
|Validation Loss|	3.63|
|Perplexity|	37.7|

Example Output:

``` bash
<|startofpoem|>
The woods were still dark,
And some birds flew and some flailed;
But one was still in the woods
And singing,
And in the trees,
On a sad song;
He was singing in a great river.
The song of the woods was the song of the wild
And when he heard
Of the wild birds,
He did not know what song it was.
A woman with a wreath stood
Heard a long song in the spring,
And sang in a voice of white to the water.
They were all together and singing
The song ...
```

2. GPT-2 Small (Last 2 Layers Trainable)

|Metric|	Value|
|------|---------|
|Validation Loss|	3.67|
|Perplexity|	39.3|

Example Output:

```bash
<|startofpoem|>
The woods were still dark,
And some birds flew and some faded
In the breeze,
And some birds glided and some faded
In the breeze,
They had not turned to flight,
And some birds flew and some faded
In the breeze,
They had not turned to flight
But rested,
And some birds flew and some faded
In the breeze,
They had not turned to flight
But sat, and some birds flew
And some faded
In the breeze,
They had not turned to flight
But rested,
And some birds flew and some faded
...
```

3. GPT-2 Medium (Last 4 Layers Trainable)

|Metric|	Value|
|------|---------|
|Validation Loss|	3.53|
|Perplexity|	34.1|

Example Output:

```bash
<|startofpoem|>
The woods were still full of the sound of the birds chirping as I walked through them, but once I was gone they were gone, they moved on their own accord.
I was glad to have changed into my bag and headed for the door to turn on the light. I turned and looked out the window until it was dark again and when I looked back I saw the moon just beginning to come back.
I heard the clatter of the door and turned. I heard something fall somewhere behind me and then everything just turned black. It sounded like a woman as she fell and I ran after
```

---

**Key Observations**

- Lower perplexity does not necessarily correspond to better poetry generation.
- Although GPT-2 Medium achieved the best validation loss and perplexity, qualitative evaluation showed that it often generated narrative prose instead of maintaining poetic structure.
- In contrast, the fully fine-tuned GPT-2 Small model produced outputs that more closely resembled poetry despite having slightly worse perplexity.
- GPT-2 can learn poetic structure from a relatively small dataset.
- Excessive layer freezing can lead to repetitive outputs.
- Perplexity should be complemented with qualitative evaluation when assessing creative writing tasks.

---

**Future Work**

- Parameter-efficient fine-tuning using LoRA.
- Style similarity metrics using sentence embeddings.
- Rhyme and meter analysis.
- Comparison against modern open-source language models.

---

This project is for educational and research purposes.

---