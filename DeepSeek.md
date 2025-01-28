# “DeepSeek R1-Zero and R1: Pioneering the Future of AI Reasoning through Reinforcement Learning”

> “The pace at which AI is evolving is both exciting and humbling. Its potential is vast, and so is our responsibility to direct it wisely.”
— Fei-Fei Li, Dept. of Comp Sci, Stanford University.

> DeepSeek paper: https://arxiv.org/pdf/2501.12948


Understanding the Modern LLM Training Pipeline
----------------------------------------------

The journey of training a Large Language Model (LLM) consists of three main phases, each serving a distinct purpose in creating an AI system capable of understanding and generating human-like text. Let's explore each phase in detail.

### Phase 1: Pre-training - Building the Foundation

The pre-training phase is where the LLM develops its fundamental understanding of language and knowledge. During this stage, the model processes an enormous amount of text data—ranging from websites and books to scientific papers and code repositories. Think of it as the model's early education, where it learns grammar, facts, and basic logical relationships.

The model learns by predicting what word comes next in a sequence, similar to how you might guess the next word in a sentence. This simple task, when performed on trillions of words, helps the model develop sophisticated language understanding. However, at this stage, the model is like a student who has read many books but doesn't yet know how to apply this knowledge to solve specific problems.

### Phase 2: Supervised Fine-tuning (SFT) - Learning to Follow Instructions

The second phase transforms the knowledgeable but unfocused model into one that can follow specific instructions and generate appropriate responses. This is accomplished through training on carefully selected examples of instructions and their ideal responses.

Think of SFT as teaching the model how to apply its knowledge in practical situations. The training data includes various tasks such as:
- Answering questions
- Writing summaries
- Generating code
- Creating creative content

The quality of these training examples is crucial—they shape how well the model will understand and respond to user requests. This is why companies invest significantly in creating high-quality training data, as it directly impacts the model's real-world performance.

### Phase 3: Preference Optimization - Refining the Output

The final phase focuses on making the model's responses more aligned with human preferences. This can be achieved through two main approaches:

1. Reinforcement Learning from Human Feedback (RLHF)
2. Direct Preference Optimization (DPO)

In both cases, the goal is to teach the model which responses humans prefer over others. This phase helps improve various aspects of the model's output, such as:
- Avoiding harmful content
- Maintaining a consistent tone
- Providing informative yet engaging responses
- Following specific behavioral guidelines

### The Evolution of "Thinking" Models

A recent advancement in LLM training is the introduction of "chain of thought" (CoT) capabilities. This approach teaches models to show their reasoning process before providing an answer. For example:

```
User: "What's the best way to transport a cake to a party?"

Model's internal thought process:
"This requires considering several factors:
1. Distance of travel
2. Weather conditions
3. Type of cake (layered, sheet, etc.)
4. Available transport options
Based on general best practices, a sturdy box with a non-slip surface
would be essential. For temperature control, keeping it cool is crucial.
A flat surface during transport will prevent sliding."

Model's response: "I recommend placing the cake in a sturdy box with a non-slip mat 
at the bottom. Keep the box level during transport, ideally on a car's floor rather 
than the seat. If it's warm outside, consider using cold packs around the box, but 
not touching the cake directly. For extra stability, you can put non-skid shelf liner 
under the box to prevent sliding."
```

This capability has gained attention with models like OpenAI's o1, which has shown remarkable performance on complex tasks like coding and mathematical problem-solving. While the exact implementation details of these "thinking" processes remain proprietary, they represent a significant advancement in how LLMs approach problem-solving.


The LLM training pipeline is a sophisticated process that transforms raw language understanding into practical problem-solving abilities. Each phase builds upon the previous one, creating increasingly capable systems that can understand context, follow instructions, and generate high-quality responses. As the field continues to evolve, new techniques and approaches will likely emerge, further improving these already impressive systems.


## DeepSeek R1-Zero and R1: Redefining AI Training for Reasoning

DeepSeek’s innovative development of R1-Zero and R1 marks a pivotal shift in training large language models (LLMs) to achieve sophisticated reasoning abilities. By challenging the conventional reliance on supervised fine-tuning, DeepSeek demonstrates how pure reinforcement learning on automatically generated training examples can unlock remarkable reasoning capabilities when applied effectively.

### R1-Zero: Pure Reinforcement Learning in Action

R1-Zero showcases the emergence of advanced reasoning capabilities solely through reinforcement learning, bypassing traditional supervised fine-tuning. Built on the DeepSeek-V3-Base architecture with 671 billion parameters, R1-Zero departs from conventional training paradigms.

#### Architectural Innovations

The R1-Zero architecture integrates 61 Transformer decoder blocks, employing a hybrid attention mechanism:

- **Dense Attention**: The first three blocks utilize dense attention for foundational pattern recognition and contextual understanding.
- **Mixture-of-Experts (MoE)**: The remaining blocks adopt a MoE architecture, enabling efficient processing of input tokens. With 256 experts per block, the model activates only 8 experts per token using a learned routing mechanism. This sparse activation pattern allows for substantial parameter scaling while controlling computational costs during inference. MoE layers, interspersed with dense layers, enable specialized subsystems for various tasks, enhancing capacity and performance.

### Training Process

The foundational DeepSeek-V3-Base model, pre-trained on 14.8 trillion tokens, served as the starting point. R1-Zero’s training employed **Group Relative Policy Optimization (GRPO)**, a reinforcement learning framework that improves upon traditional methods like Proximal Policy Optimization (PPO).

#### Understanding GRPO

GRPO eliminates the need for a value model by sampling multiple outputs for each input and using the group’s average reward as the baseline. This simplifies advantage estimation, making reinforcement learning more efficient. For example, if 64 outputs for a math problem yield an average reward of 0.7, and one solution scores 0.9, the solution receives a positive advantage of 0.2. This approach removes reliance on separate value models and streamlines training.

A standout feature of GRPO is the spontaneous development of **self-verification behaviors**. During training, the model begins to recognize and correct its own errors, often stating, “Wait, I notice an error in my previous step...” before revising its reasoning. This behavior emerges naturally, driven by the group-based reward structure.

#### Reward Structure

The reward structure comprises:

1. **Accuracy Rewards**: Evaluates the correctness of responses. For example, math solutions are verified based on predefined formats, while coding problems are validated using compilers and test cases.
2. **Format Rewards**: Encourages structured reasoning by requiring thought processes to be encapsulated within specific tags (e.g., `<think>` and `</think>`).

This fully automated system eliminates the need for human feedback, enabling scalable and unbiased training.

### Addressing R1-Zero’s Limitations

Despite its achievements, R1-Zero exhibited challenges:
- **Readability**: Responses were logically sound but often fragmented or unclear.
- **Language Mixing**: The model frequently switched languages mid-response, particularly between English and Chinese. While single-language enforcement slightly degraded reasoning performance, it improved user-friendliness.

### DeepSeek R1: A Multi-Stage Training Pipeline

Building on R1-Zero, DeepSeek R1 employs a four-stage training process to address these limitations while retaining strong reasoning capabilities:

1. **Cold-Start Stage**: Researchers curated a small dataset of detailed chain-of-thought (CoT) examples through:
   - Few-shot prompting with CoT samples.
   - Outputs from R1-Zero, refined and formatted for readability.
   - Post-processing by human annotators.
   
   These examples were used to fine-tune DeepSeek-V3-Base, stabilizing the early training phase.

2. **Reasoning Reinforcement Learning**: Building on GRPO, this stage focused on mathematical, logical, and coding tasks. Automatic correctness verification ensured high-quality training data. Language consistency rewards reduced language mixing issues.

3. **General Capability Fine-Tuning**: Beyond reasoning, this stage expanded the model’s versatility. Researchers:
   - Curated reasoning prompts and generated trajectories using rejection sampling.
   - Filtered outputs for clarity and consistency.
   - Integrated non-reasoning data, such as writing and translation, from the DeepSeek-V3 pipeline.

   Approximately 800,000 examples were used to fine-tune the model over two epochs.

4. **Preference Optimization Reinforcement Learning**: The final stage optimized the model’s preferences for generating coherent, user-friendly outputs.

### Conclusion

DeepSeek’s R1-Zero and R1 represent breakthroughs in AI reasoning through innovative training methodologies and architectural designs. R1-Zero’s success with pure reinforcement learning and R1’s refined multi-stage process demonstrate that extensive supervised training is not essential for developing sophisticated reasoning abilities. These advancements, combined with cost efficiency and scalability, signal a promising future for AI research and development. The lessons from R1’s journey will undoubtedly influence the next generation of AI models.

