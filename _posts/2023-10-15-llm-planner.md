---
title: 'LLM-Planner: Few-Shot Grounded Planning for Embodied Agents with Large Language Models'
date: 2023-10-15
permalink: /posts/2023/10/2023-10-15_llm_planner/
tags:
  - LLM
  - LLM planning
---

This paper introduces LLM-Planner, which utilizes LLMs as high-level planners for embodied agents, allowing them to generate and adapt plans according to the current environment. Experiments on the ALFRED dataset show that using less than 0.5% of paired training data, LLM-Planner achieves competitive performance with recent baselines that are trained using the full training data.

<div role="note" style="display: flex;"><div style="display: flex; width: 100%; border-radius: 3px; background: rgb(241, 241, 239); padding: 16px 16px 16px 12px;"><div><div role="button" tabindex="0" class="notion-record-icon notranslate" aria-label="💡 Change callout icon" style="user-select: none; transition: background 20ms ease-in 0s; cursor: pointer; display: flex; align-items: center; justify-content: center; height: 24px; width: 24px; border-radius: 0.25em; flex-shrink: 0;"><div style="display: flex; align-items: center; justify-content: center; height: 24px; width: 24px;"><div style="height: 16.8px; width: 16.8px; font-size: 16.8px; line-height: 1; margin-left: 0px; color: black;"><img class="notion-emoji" alt="💡" aria-label="💡" src="data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==" style="width: 100%; height: 100%; background: url(&quot;/images/emoji/twitter-emoji-spritesheet-64.d3a69865.png&quot;) 47.4576% 25.4237% / 6000% 6000%;"></div></div></div></div><div style="display: flex; flex-direction: column; min-width: 0px; margin-left: 8px; width: 100%;"><details><summary>Table of contents</summary><div data-block-id="057081a8-705c-4c90-bed1-63e6d86eb4c7" class="notion-selectable notion-table_of_contents-block" style="width: 100%; max-width: 100%; margin-top: 4px; margin-bottom: 0px;"><div contenteditable="false" data-content-editable-void="true" style="position: relative;"><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#link-to-project-page" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Link to project page </div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#abstract" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Abstract</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#problem-statement" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Problem Statement</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#methodology" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Methodology</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#overview" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Overview</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#1-prompt-design" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">1. Prompt Design</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#2-in-context-example-retrieval" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">2. In-context Example Retrieval</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#3-grounded-re-planning" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">3. Grounded Re-planning</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#4-integration-with-existing-vision-and-language-navigation-vln-models" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">4. Integration with Existing Vision-and-Language Navigation (VLN) models</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#results" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Results</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#reference" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Reference</div></div></a></div></div></div></details></div></div></div>

<br />

# **Link to project page**

[LLM-Planner: Few-Shot Grounded Planning with Large Language Models](https://osu-nlp-group.github.io/LLM-Planner/)

# Abstract

- The study focuses on using LLMs as a **high-level planner** for embodied agents that can follow natural language instructions to complete complex tasks in a visually-perceived environment
- A novel method, **LLM-Planner**, is proposed to perform **few-shot high-level planning** for embodied agents.
- The LLMs are enhanced with **physical grounding** to **generate and update plans** that are grounded in the current environment.
- Experiments on the ALFRED dataset show that using less than **0.5% of paired training data**, LLM-Planner achieves competitive performance with recent baselines that are trained using the full training data.
- This work opens the door for developing versatile and sample-efficient embodied agents that can quickly learn many tasks.

# Problem Statement

- Before LLM era, language driven agents require a **large number of labeled samples** to learn each task
- Recently, LLM-based agents have shown great few-shot learning abilities. However they are evaluated in **limited evaluation setting**:
    - Example: evaluated in two environments with 15 object types
- Besides, current work mostly generate a **single static plan** from the language instruction, instead of dynamically adjust the plan based on the feedback from the environment

# Methodology

## Overview

- **Design appropriate prompt:**
    - Appropriate prompt helps to guide LLM to generate high-level plans (HLP)s
- **kNN retriever:**
    - The authors adopt kNN to retrieve similar examples for LLM to perform in-context learning
- **Grounded re-planning algorithm:**
    - Grounded re-planning algorithm is used to enhance LLMs' ability to adapt to the environment, improving HLP quality

![Untitled](/images/LLM-Planner%20Few-Shot%20Grounded%20Planning%20for%20Embodie%20b1f1971e417c4c52b3174a1a5d9e4842/Untitled.png)

## 1. Prompt Design

As shown in Figure 2, The prompt begins with:

- An intuitive explanation of the task + list of allowable high-level actions.
- Next, in-context examples selected by the kNN retriever, consists of:
    - “Task description: [high-level goal instruction].”
    - “Step-by step instructions (optional): [step-by-step instructions]”
    - Dynamic grounded re-planning, consists of:
        - “Completed plan: [sub-goals that have been completed]”
        - “Visible objects: [observed objects]”
- Finally, we append the test example in the same format that ends with “Next plan:”

## 2. In-context Example Retrieval

- High quality in-context examples can improve performance of the LLM-agent
- Intuitively if the current task is to “*cook a potato*,” an in-context example demonstrates “*cooking an egg*” is likely more informative than one that demonstrates how to “*clean a plate*”
- Frozen BERT-base model is used to generate the embedding for the test example.
    - Next, Euclidean distance is used to measure the similarity between the tasks
    - The *K* most similar examples to the current task are selected as context examples.

## 3. Grounded Re-planning

- Static high-level planning lacks grounding to physical environment, which lead to:
    - the agent fails to execute an action (e.g., bumping into a wall)
    - take long time and fail to accomplish a task (e.g., wandering endlessly)
- Re-planning will be triggered under 2 conditions:
    - agent fails to execute an action
    - after fixed number of steps
- The re-planning algorithm will generate a new plan based on the partially completed HLP, to help the agent unstuck

## 4. Integration with Existing Vision-and-Language Navigation (VLN) models

- VLN task is defined as following:
    - Given a language instruction *I*, an agent needs to predict and carry out **a sequence of primitive actions in the environment *E* to accomplish the task**
- The authors integrated LLM-Planner with existing VLN models, **HLSM** to turn the HLP from LLM-Planner into low-level plan

<p align="center">
  <img src="/images/LLM-Planner%20Few-Shot%20Grounded%20Planning%20for%20Embodie%20b1f1971e417c4c52b3174a1a5d9e4842/Untitled%201.png" alt="Image Description">
</p>

# Results

**Metrics**

1. Success rate (SR): percentage of tasks fully completed by the agents
2. High-level planning accuracy (HLP ACC)
3. Goal-condition success rate (GC)

<p align="center">
  <img src="/images/LLM-Planner%20Few-Shot%20Grounded%20Planning%20for%20Embodie%20b1f1971e417c4c52b3174a1a5d9e4842/Untitled%202.png" alt="Image Description">
</p>

# Reference

1. Song et al. “[LLM-Planner: Few-Shot Grounded Planning for Embodied Agents with Large Language Models](https://arxiv.org/abs/2212.04088)”, ICCV 2023