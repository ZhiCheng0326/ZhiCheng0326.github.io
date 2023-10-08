---
title: 'Notes on Recent Talks about Autonomous Intelligence by Yann LeCun'
date: 2023-10-08
permalink: /posts/2023/10/2023-10-08_world_model/
tags:
  - JEPA
---
This note includes insights from Yann LeCun, often referred to as the father of deep learning. In his talk, he discussed the limitations of current machine learning methods and self-supervised learning methods. He emphasized the need for objective-driven AI and introduced the concept of a modular cognitive architecture, also known as the **world model**. Additionally, he introduced the **Joint-Embedding Predictive Architecture (JEPA)**, a new approach in the field.

<div role="note" style="display: flex;"><div style="display: flex; width: 100%; border-radius: 3px; background: rgb(241, 241, 239); padding: 16px 16px 16px 12px;"><div><div role="button" tabindex="0" class="notion-record-icon notranslate" aria-label="💡 Change callout icon" style="user-select: none; transition: background 20ms ease-in 0s; cursor: pointer; display: flex; align-items: center; justify-content: center; height: 24px; width: 24px; border-radius: 0.25em; flex-shrink: 0;"><div style="display: flex; align-items: center; justify-content: center; height: 24px; width: 24px;"><div style="height: 16.8px; width: 16.8px; font-size: 16.8px; line-height: 1; margin-left: 0px; color: black;"><img class="notion-emoji" alt="💡" aria-label="💡" src="data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==" style="width: 100%; height: 100%; background: url(&quot;/images/emoji/twitter-emoji-spritesheet-64.d3a69865.png&quot;) 47.4576% 25.4237% / 6000% 6000%;"></div></div></div></div><div style="display: flex; flex-direction: column; min-width: 0px; margin-left: 8px; width: 100%;"><details><summary>Table of contents</summary><div data-block-id="6763599a-821d-40b6-aedf-8728525bb897" class="notion-selectable notion-table_of_contents-block" style="width: 100%; max-width: 100%; margin-top: 4px; margin-bottom: 0px;"><div contenteditable="false" data-content-editable-void="true" style="position: relative;"><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#introduction" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Introduction</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#the-limitation-of-machine-learning" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">The limitation of machine learning</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#self-supervised-learning-ssl" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Self-supervised Learning (SSL)</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#what-is-ssl" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">What is SSL?</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#why-is-ssl-effective-in-text-but-not-as-much-in-images" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Why is SSL effective in text but not as much in images?</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#generative-ai-and-auto-regressive-llm" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Generative AI and Auto-Regressive LLM</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#autoregressive-generative-architectures" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Autoregressive Generative Architectures</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#the-limitations-of-autoregressive-llm" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">The limitations of Autoregressive LLM</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#autoregressive-are-doomed" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Autoregressive are doomed</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#three-challenges-for-ai--ml-in-the-future" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Three Challenges for AI &amp; ML in the future</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#objective-driven-ai" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Objective-Driven AI</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#modular-cognitive-architecture" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Modular Cognitive Architecture</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#perception-action-system" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Perception-Action system</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#perception-planning-action-system" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Perception-Planning-Action system</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#non-deterministic-world-model" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Non-Deterministic World Model</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#hierarchical-planning" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Hierarchical Planning</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#outlook-for-objective-driven-ai-system" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Outlook for Objective Driven AI System</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#building--training-the-world-model" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Building &amp; Training the World Model</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#joint-embedding" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Joint Embedding</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#joint-embedding-architectures-variants" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Joint Embedding Architectures Variants</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#energy-based-models" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Energy-Based Models</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#contrastive-method" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Contrastive method</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#regularized-method" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Regularized method</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#recommendations" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Recommendations</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#training-a-joint-embedding-predictive-architecture-jepa-with-regularized-methods" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 24px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Training a Joint-Embedding Predictive Architecture (JEPA) with Regularized Methods </div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#vicreg-variance-invariance-covariance-regularization" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 48px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">VICReg: Variance, Invariance, Covariance Regularization</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#problems-to-be-solved" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Problems to be solved</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#conclusion" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Conclusion</div></div></a></div><div style="color: rgb(120, 119, 116); fill: rgb(120, 119, 116);"><a href="#reference" rel="noopener noreferrer" style="display: block; color: inherit; text-decoration: none; user-select: none; transition: background 20ms ease-in 0s; cursor: pointer;"><div style="padding: 6px 2px; font-size: 14px; line-height: 1.3; display: flex; align-items: center; margin-left: 0px;"><div class="notranslate" style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background-image: linear-gradient(to right, rgba(55, 53, 47, 0.16) 0%, rgba(55, 53, 47, 0.16) 100%); background-repeat: repeat-x; background-position: 0px 100%; background-size: 100% 1px;">Reference</div></div></a></div></div></div></details></div></div></div>

<br />

# Introduction

## The limitation of machine learning

- Supervised learning requires many label data
- Reinforcement learning requires many trials
- Self-supervised learning only works well with text/other discrete modalities

**Compare with human and animals:**

- learn new tasks quickly
- can reason and plan
- have common sense
- their behavior is objective driven

## Self-supervised Learning (SSL)

### What is SSL?

- Learning to **fill in the blanks**
- Example in NLP domain:
    - Sentence is masked/corrupted:
        - The sun was shining brightly in the clear blue sky. → The sun was shining ____ in the clear blue ____ .
- In the process of learning to fill in the blank, the model **learned the representation of natural language**

### Why is SSL effective in text but not as much in images?

- Natural language is finite, finite amount of vocabulary
- Natural language is discrete

## Generative AI and Auto-Regressive LLM

### Autoregressive Generative Architectures

- Predict next token based on previous tokens
- Tokens can **represent words, image patches,** …

### The limitations of Autoregressive LLM

- Hallucinations
- Logical errors and inconsistency
- Limited reasoning and planning
- LLM have limited knowledge of underlying reality, as they have no common sense and can’t plan their answer

**Compare with human and animals:**

- Understand how the world works
- Can predict consequences of their actions
- Can perform chain of reasoning with unlimited number of steps
- Can plan complex tasks by decomposing into sequences of subtasks

### Autoregressive are doomed

$$
P(correct) = (1-e)^n
$$

where $e$ is probability of wrong tokens produced.

- This ***diverges exponentially***
- It’s ***not fixable without major redesign***

## Three Challenges for AI & ML in the future

1. **Learning representations and predictive models of the world**
- Learning to represent the world in a non task-specific way
- Learning predictive models for planning and control

1. **Learning to reason**
- Making reasoning and planning as energy minimization

1. **Learning to plan complex actions to satisfy objectives**
- Learning hierarchical representations of action plans


# Objective-Driven AI
## **Modular Cognitive Architecture**

An architecture of different modules interact with each other

- **Perception module**:
    - Computes representation of the state of the world from perception (possibly combined with memory)
- **World model module**:
    - Predict the outcomes of series of actions given by the actor
- **Actor module**:
    - Imagine a series of actions and feed to the world model
- **Cost module**:
    - Evaluate the outcomes from the world model, measuring the quality of the outcomes

<p align="center">
  <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled.png" alt="Image Description">
</p>

## Perception-Action system

The purpose of the agent is to figure a sequences of actions that minimizes the cost during inference time. Therefore, inference is also an optimization process.

- **Task objective**: Measures divergence to goal
- **Guardrail objective**: Ensure trustworthy AI

<p align="center">
  <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%201.png" alt="Image Description">
</p>

## Perception-Planning-Action system

- think of this as multi-step or recurrent world model
- Same world model applied at multiple time steps with guardrail costs applied to every timestep.
- Similar idea with Model Predictive Control (MPC)

<p align="center">
  <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%202.png" alt="Image Description">
</p>

### Non-Deterministic World Model

- The world is not deterministic, therefore we need to introduce latent variables to help capture the diversity
- So it can be multiple predictions for a single action

<p align="center">
  <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%203.png" alt="Image Description">
</p>

## Hierarchical Planning

- We require a system capable of learning diverse levels of representations of the world's state, enabling it to effectively decompose complex tasks, **without explicitly designing the hierarchy**
- Low-level representations only predict in the short term
    - Too much details
    - Prediction is hard
- High-level representations predicts in the longer term
    - Less details
    - Prediction is easier

<p align="center">
  <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%204.png" alt="Image Description">
</p>

## Outlook for Objective Driven AI System

- If we had a system that was able to:
    1. Receive a query
    2. Conduct planning in the abstract representation space
    3. Then translate the representation into fluent text using autoregressive decoder, then 
- If we have such system:
    - We could have a AI model that is factual, fluent, non-toxic, etc.
    - No need for RLHF or fine-tuning, because the model is constrained by the guardrail cost modules

# Building & Training the World Model

Things that are **easy for humans** are **difficult for AI** and vice versa, we are **missing something big**!

- Using SSL in the case of video prediction:
    - The predicted video frame is blurry, because the system is trained to make one prediction, which is an average of all the possible futures
        
        <p align="center">
            <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%206.png" alt="Image Description">
        </p>

## Joint Embedding

- Generative method:
    - Encode input $x$ to get representation $S_x$ to predict variable $\tilde y$, then measure the divergence between ground true $y$ and predicted $y$
- Joint Embedding method:
    - Encode input $x$ to get representation $S_x$, then **predict representation $\tilde S_y$**, then **measure the divergence between $S_y$ and  $\tilde S_y$**
    - Encoder $y$ has invariant properties:
        - Map multiple $y$ into same $S_{y}$, therefore if $y$ is hard to predict, the encoder can eliminate the noisy information, only focus on the details relevant to the task
    
    <p align="center">
            <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%207.png" alt="Image Description">
    </p>
    
### Joint Embedding Architectures Variants

- left: without predictor
- middle: with predictor
- right: with latent variable
- To train these variants, it might collapse
    - Because we want the representations of $x$ and $y$, that is $S_x$ and $S_y$ to be identical
    - No matter what the input $x$ and $y$ are, $S_x$ and $S_y$ always constant

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Image_20230910103233.png" alt="Image Description">
</p>

## Energy-Based Models

- Assign lower energy to region near the data points
- Assign higher energy to energy outside of those data points (outliers)
- If there exists a function that can model the energy landscape, that function captured the dependencies between $x$ and $y$

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled_(1).png" alt="Image Description">
</p>

### **Contrastive method**

- Train the model so that it gives **low energy** to the **data point with higher density** and **high energy** to the **two contrastive green dots**
- Disadvantage:
    - In high dimensional space, the **number of contrastive points grows exponentially** for the energy function to capture the right shape

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Screenshot_2023-10-02_180542_(2).png" alt="Image Description">
</p>

### Regularized method

- By introducing regularization, the energy function gives low energy to **small volume** of space

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled_(2)_(1).png" alt="Image Description">
</p>

## Recommendations

1. Instead of generative models, opt for joint-embedding architectures
2. Instead of probabilistic model, opt for energy-based models
3. Instead of contrastive methods, opt for regularized methods
4. Instead of reinforcement learning, opt for model-predictive control
    1. Use RL only when planning doesn’t yield predicted outcome, to adjust the world model or the critic

## Training a Joint-Embedding Predictive Architecture (JEPA) with Regularized Methods

- 4 terms in the cost function:
    - Maximize information of $S_x$
    - Maximize information of $S_y$
    - Minimize information of latent variable $z$
    - Minimize prediction error
- However, we it’s very hard to train with that cost function because we don’t have lower bound for those information

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled_(3)_(1).png" alt="Image Description">
</p>

### VICReg: **Variance, Invariance, Covariance Regularization**

To overcome the previous issue where we have no lower bound for the information content, we:

1. Make sure the variance of every component of $S_x$ is at least one
2. Make sure the components of $S_x$ are decorrelated

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Image_20230910105640.png" alt="Image Description">
</p>

# Problems to be solved

<p align="center">
        <img src="/images/Notes%20on%20Recent%20Talks%20about%20Autonomous%20Intelligenc%20a6be32de51274fc99fb0ab623140251e/Untitled%208.png" alt="Image Description">
</p>

# Conclusion

- We are still missing essential concepts to reach human-level AI
    - Scaling up auto-regressive LLM will not take us there
- Learning World Models with SSL and JEPA
    - Non-generative architecture, predicts in representation space
- Objective-driven AI Architectures
    - Can plan their answers
    - Must satisfy objectives: are steerable and controllable
    - Guardrail objectives can make them safe

# Reference

1. “[The Impact of chatGPT talks (2023) - Keynote address by Prof. Yann LeCun (NYU/Meta)](https://www.youtube.com/watch?v=vyqXLJsmsrk&ab_channel=MITDepartmentofPhysics)”, YouTube 
2. “**[Yann LeCun, Chief AI Scientist at Meta AI: From Machine Learning to Autonomous Intelligence](https://www.youtube.com/watch?v=mViTAXCg1xQ&t=191s&ab_channel=InstituteforExperientialAI)**”, YouTube