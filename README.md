### Chapter 1
Reading the chapter

### Chapter 2 (Generating Text with a Pre-Trained LLM):
- Loaded Qwen3
- Made it generate some text
- Looked at methods to speedup inference:
    1. KV caching (x4)
    2. Model compilation (x2) (Not working at the moment, will have to install Visual Studio Build Tools with the "C++ workload" and run Python from the "x64 Native Tools" prompt)


### Chapter 3 (Evaluating Reasoning Models):
- Wrapped text gen function
- Learnt how to extract and normalize final output of LLM for math questions
- Testing function for math dataset
  

### Chapter 4 (Improving Reasoning with Inference-Time Scaling):
- Explored 3 methods:
    1. CoT prompting
    2. Temp scaling + Top p selection
    3. Self refinement (majority vote)

 
### Chapter 5 (Inference-Time Scaling Via Self-Refinement)
- Scoring LLM with rules
- Scoring responses based on confidence (logprob)
- Self refinement with iterative feedback


### Chapter 6 (Training Reasoning Models with Reinforcement Learning):
- RLVR using GRPO
- GRPO stages:
      1. Rollouts
      2. Rewards
  <math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <msub>
    <mtext>advantages</mtext>
    <mi>i</mi>
  </msub>
  <mo>=</mo>
  <mfrac>
    <mrow>
      <msub>
        <mi>r</mi>
        <mi>i</mi>
      </msub>
      <mo>&#x2212;</mo>
      <msub>
        <mi>&#x3BC;</mi>
        <mi>r</mi>
      </msub>
    </mrow>
    <mrow>
      <msub>
        <mi>&#x3C3;</mi>
        <mi>r</mi>
      </msub>
      <mo>+</mo>
      <mi>&#x3F5;</mi>
    </mrow>
  </mfrac>
</math>

      3. Score rollouts with log-probs
  
      4. Policy gradient loss (-A log P)
  <math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <msub>
    <mrow data-mjx-texclass="ORD">
      <mi data-mjx-variant="-tex-calligraphic" mathvariant="script">L</mi>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <mrow data-mjx-texclass="ORD">
        <mi data-mjx-auto-op="false">PG</mi>
      </mrow>
    </mrow>
  </msub>
  <mo>=</mo>
  <mo>&#x2212;</mo>
  <mfrac>
    <mn>1</mn>
    <mi>N</mi>
  </mfrac>
  <munderover>
    <mo data-mjx-texclass="OP">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>i</mi>
      <mo>=</mo>
      <mn>1</mn>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <mi>N</mi>
    </mrow>
  </munderover>
  <msub>
    <mi>A</mi>
    <mi>i</mi>
  </msub>
  <munderover>
    <mo data-mjx-texclass="OP">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>t</mi>
      <mo>=</mo>
      <mn>1</mn>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <msub>
        <mi>T</mi>
        <mi>i</mi>
      </msub>
    </mrow>
  </munderover>
  <mi>log</mi>
  <mo data-mjx-texclass="NONE">&#x2061;</mo>
  <msub>
    <mi>p</mi>
    <mi>W</mi>
  </msub>
  <mstyle>
    <mspace width="-0.167em"></mspace>
  </mstyle>
  <mrow data-mjx-texclass="INNER">
    <mo data-mjx-texclass="OPEN">(</mo>
    <msubsup>
      <mi>y</mi>
      <mi>t</mi>
      <mrow data-mjx-texclass="ORD">
        <mo stretchy="false">(</mo>
        <mi>i</mi>
        <mo stretchy="false">)</mo>
      </mrow>
    </msubsup>
    <mo>&#x2223;</mo>
    <msubsup>
      <mi>y</mi>
      <mrow data-mjx-texclass="ORD">
        <mo>&lt;</mo>
        <mi>t</mi>
      </mrow>
      <mrow data-mjx-texclass="ORD">
        <mo stretchy="false">(</mo>
        <mi>i</mi>
        <mo stretchy="false">)</mo>
      </mrow>
    </msubsup>
    <mo>,</mo>
    <msup>
      <mi>x</mi>
      <mrow data-mjx-texclass="ORD">
        <mo stretchy="false">(</mo>
        <mi>i</mi>
        <mo stretchy="false">)</mo>
      </mrow>
    </msup>
    <mo data-mjx-texclass="CLOSE">)</mo>
  </mrow>
</math>

- Training loop for GRPO (backprop through log probs not advantages)

