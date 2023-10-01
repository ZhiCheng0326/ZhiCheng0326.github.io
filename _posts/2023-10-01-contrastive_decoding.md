---
title: 'Contrastive Decoding: Open-ended Text Generation as Optimization'
date: 2023-10-01
permalink: /posts/2023/10/2023-10-01_contrastive_decoding/
tags:
  - LLM
  - LLM reasoning
---

The paper proposes a new decoding method for open-ended text generation, called contrastive decoding (CD), which aims to generate text that is fluent, coherent, and informative, by exploiting the contrasts between expert model and amateur model behaviors.

<div role="note" style="display: flex;"><div style="display: flex; width: 100%; border-radius: 3px; background: rgb(241, 241, 239); padding: 16px 16px 16px 12px;"><div><div role="button" tabindex="0" class="notion-record-icon notranslate" aria-label="💡 Change callout icon" style="user-select: none; transition: background 20ms ease-in 0s; cursor: pointer; display: flex; align-items: center; justify-content: center; height: 24px; width: 24px; border-radius: 0.25em; flex-shrink: 0;"><div style="display: flex; align-items: center; justify-content: center; height: 24px; width: 24px;"><div style="height: 16.8px; width: 16.8px; font-size: 16.8px; line-height: 1; margin-left: 0px; color: black;"><img class="notion-emoji" alt="💡" aria-label="💡" src="data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==" style="width: 100%; height: 100%; background: url(&quot;/images/emoji/twitter-emoji-spritesheet-64.d3a69865.png&quot;) 47.4576% 25.4237% / 6000% 6000%;"></div></div></div></div><div style="display: flex; flex-direction: column; min-width: 0px; margin-left: 8px; width: 100%;"><div class="notranslate" spellcheck="true" placeholder="Press ‘space’ for AI, ‘/’ for commands…" data-content-editable-leaf="true" style="max-width: 100%; width: 100%; white-space: pre-wrap; word-break: break-word; caret-color: rgb(55, 53, 47); padding-left: 2px; padding-right: 2px;" contenteditable="true"><span style="font-weight:600" data-token-index="0" class="notion-enable-hover">Table of Contents</span></div><div data-block-id="2c2b23bd-b4b4-4e2c-ac50-8d14e8d6a4e6" class="notion-selectable notion-table_of_contents-block" style="width: 100%; max-width: 100%; margin-top: 4px; margin-bottom: 0px;"><div contenteditable="false" data-content-editable-void="true" style="position: relative;"><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#abstract" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Abstract</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#what-is-the-pain-point-that-the-author-tries-to-solve" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">What is the pain point that the author tries to solve?</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#solution" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Solution</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#methodology" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Methodology</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#adaptive-plausibility-constraint" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Adaptive Plausibility Constraint</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#full-method" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Full Method</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#choice-of-amateur" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Choice of Amateur</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#results" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Results</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#reference" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Reference</div></div></a></div></div></div></div></div></div>  

<br />
# Abstract

- The paper proposes a new decoding method for open-ended text generation, called contrastive decoding (CD).
- CD measures the difference between the log-probabilities of a large model (expert) and a small model (amateur), subject to a plausibility constraint that filters out low-probability tokens under the expert.
- CD aims to generate text that is fluent, coherent, and informative, by exploiting the contrasts between expert and amateur behaviors.
- CD requires **no additional training** and **works across different model scales and domains**.

<p align="center">
  <img src="/images/2023-10-01-contrastive_decoding-img.png" alt="Image Description">
</p>

# What is the pain point that the author tries to solve?

- Generated text from LLM is prone to **incoherence** and **topic drift** due to poor sampling choices over long sequences
- Maximizing probability in sequence often results in **short**, **repetitive** and **tedious** text

# Solution

- Author proposes contrastive decoding (CD), which searches for text that **maximizes the difference** between **expert** log-probabilities **and amateur** log-probabilities, with restricted search space
- Why take the max difference between expert and amateur log-probabilities?
    - Smaller LLM gives high probability to short, repetitive, irrelevant, uninteresting tokens
    - Larger LLM gives high probability to desirable outputs
    - Hence, by getting the max difference between expert and amateur model, we can improve text generation
- Advantage of CD:
    - **No training required**, compared to unlikelihood training and contrastive learning proposed in other paper

# Methodology

- Expert model gives high probability to good, non-repetitive tokens, whereas amateur model gives high probability to undesired tokens
- We want to ***reward text patterns favored by the expert LMs*** and ***penalizes patterns favored by the small amateur LMs***. Therefore, the author proposed Contrastive objective, $L_{CD}(x_{\text{cont}}, x_{\text{pre}})$:

$$
\log p_{\text{EXP}}(x_{\text{cont}} | x_{\text{pre}}) - \log p_{\text{AMA}}(x_{\text{cont}} | x_{\text{pre}})
$$

- If tokens from small LMs not favorable, why don’t we penalize amateur LMs completely?
    - Small LMs still capture simple aspects of English grammar and common sense
    - The author introduced plausibility constraint to complement CD objective

## Adaptive Plausibility Constraint

$$
V_{\text{head}}(x_{<i}) = \{x_i \in V : p_{\text{EXP}}(x_i | x_{<i}) \geq \alpha \max_{w} p_{\text{EXP}}(w|x_{<i})\}
$$

- The constraint only keeps tokens that have probability **greater than or equal to a fraction α of the maximum probability token under the expert model**
- $\alpha$ in the range of [0,1], it truncates next token distribution of $p_{EXP}$
    - large $\alpha$, keep only tokens with high probabilities
    - small $\alpha$, allows lower probabilities tokens to be considered
    - $\alpha = 0.1$ is used in this paper.
        - So, it only keeps 10% of the most likely token of the expert model
    

## Full Method

$$
\text{CD-score}(x_i; x_{<i}) = \begin{cases} \log \frac{p_{\text{EXP}}(x_i|x_{<i})}{p_{\text{AMA}}(x_i|x_{<i})}, & \text{if } x_i \in V_{\text{head}}(x_{<i}), \\-\infty, & \text{otherwise}.\end{cases}
$$

## Choice of Amateur

We should select the amateur LM that downplays behaviors from the expert LM. Three aspects to consider:

1. Scale: We prefer small scale LMs because they are more prone to errors
2. Temperature: We prefer $\tau$ close to 0 because it highlights the mode of the amateur distribution, which is more prone to errors
3. Context window: Short context length. To weaken the coherence of the amateur LMs

# Results

Generated text are more diverse and higher quality when using XL model size as teacher, small model size as student 

<p align="center">
  <img src="/images/2023-10-01-contrastive_decoding-img1.png" alt="Image Description">
</p>
<br />
<p align="center">
  <img src="/images/2023-10-01-contrastive_decoding-img2.png" alt="Image Description">
</p>
<br />
<p align="center">
  <img src="/images/2023-10-01-contrastive_decoding-img3.png" alt="Image Description">
</p>

# Reference

1. Li et al. “[Contrastive Decoding: Open-ended Text Generation as Optimization](https://arxiv.org/abs/2210.15097)”, ACL 2023