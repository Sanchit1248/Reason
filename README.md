# Chapter 1
Understanding the pipeline



# Chapter 2 (Generating Text with a Pre-Trained LLM):
- Loaded Qwen3
- Made it generate some text
- Looked at methods to speedup inference:
    1. KV caching (x4)
    2. Model compilation (x2) (Not working at the moment, will have to install Visual Studio Build Tools with the "C++ workload" and run Python from the "x64 Native Tools" prompt)



# Chapter 3 (Evaluating Reasoning Models):
- Wrapped text gen function
- Learnt how to extract and normalize final output of LLM for math questions
- Testing function for math dataset


  
# Chapter 4 (Improving Reasoning with Inference-Time Scaling):
- Explored 3 methods:
    1. CoT prompting
    2. Temp scaling + Top p selection
    3. Self refinement (majority vote)


 
# Chapter 5 (Inference-Time Scaling Via Self-Refinement)
- Scoring LLM with rules
- Scoring responses based on confidence (logprob)
- Self refinement with iterative feedback
  


# Chapter 6 — Training Reasoning Models with Reinforcement Learning

## RLVR using GRPO

### GRPO Stages

1. Generate rollouts

2. Compute rewards

$$ A_i = \frac{r_i - \mu_r}{\sigma_r + \epsilon} $$

3. Score rollouts using sequence log-probabilities

4. Policy gradient loss ($-A \log P$)

$$ \mathcal{L}_{PG} = -\frac{1}{N} \sum_{i=1}^{N} A_i \sum_{t=1}^{T_i} \log p_W \left( y_t^{(i)} \mid y_{<t}^{(i)}, x^{(i)} \right) $$

### Training Loop

Backpropagation occurs through the sequence log-probabilities, **not through the advantages**.
