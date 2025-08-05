## AI

## <a name='table-of-contents'></a>Table of Contents

<!-- vscode-markdown-toc -->
- [AI](#ai)
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
- [Basics](#basics)
  - [History of AI](#history-of-ai)
  - [How does AI Learn](#how-does-ai-learn)
  - [Types of AI](#types-of-ai)
  - [Augmented Intelligence](#augmented-intelligence)
  - [Branches of AI](#branches-of-ai)
  - [AI Agents](#ai-agents)
  - [Robotics](#robotics)
  - [Prompts](#prompts)
- [Brief](#brief)
  - [Generative AI](#generative-ai)
  - [Prompt Engineering](#prompt-engineering)
- [Key Concepts](#key-concepts)
- [Popular Algorithms](#popular-algorithms)
- [Tools and Libraries](#tools-and-libraries)
- [References](#references)
<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Introduction'></a>Introduction
[🔝](#table-of-contents)
- Simulations of human intelligence through computer systems.
- Utilizes algorithms and data to function
- Enables machines to perform tasks requiring human intelligence.

## <a name='Basics'></a>Basics
[🔝](#table-of-contents)

### <a name='HistoryofAI'></a>History of AI
- `1950s`: 
  - Alan Turing's Test
  - McCarthy coined "Artificial Intelligence"
- `1980s`:
    - Machine Learning boom
- `1990s`:
    - Neural Networks
- `2000s`:
    - Deep Learning's rise
- `2010s`:
    - NLP and Computer Vision
- `2020s`:
    - Deep Learning Models, Autonomous Systems and Healthcare Applications.  

### <a name='Howdoesailearn'></a>How does AI Learn
- `Supervised Learning`: When algorithm is trained based on human labeled data, more the samples, better the model
    - Types of supervised learning
        - `Regression`: Models the relationship between input features (x) and a continuous output variable (y). *Regression is used to estimate or predict continuous values.*
        - `Classification`: Assigns discrete class labels (y) to input features (x). *Classification focuses on identifying which category or class an input belongs to.*
        - `Neural Network`: *Structures that imitate the human brain to process input data*, recognize patterns, and make decisions or predictions. Neural networks can be used for both regression and classification tasks.
- `Unsupervised Learning`: Relies on giving the algorithm unlabeled data and it finds the patterns itself, useful for clustering similar data points and detecting anomalies.
- `Reinforcement Learning`: The algorithm is given a set of rules, goals, allowed actions, and constraints. It learns by trying different actions, receiving rewards for good decisions and penalties for bad ones, aiming to maximize its total reward. Used for tasks like teaching a machine to play chess or navigate an obstacle course.
- Training a model involves splitting a dataset into training, validation, and testing sets.
    - `Training set`: Trains the algorithm
    - `Validation set`: Fine-tunes and validates the model
    - `Test set`: Evaluates the model's performance

### <a name='TypesofAi'></a>Types of AI
- `Strength`:
  1. `Narrow/Weak AI` (narrow AI)
      - AI tailored for specific domains
      - Decision-making based on programmed algorithms and training data
      - Ex: Translator, Recommendation System
  2. `General/Strong AI` (generalized AI)
      - An AI with diverse capabilities across unrelated tasks
      - Acquires new skills to face new challenges
      - Is a combination of various AI strategies
      - Ex: Finance, HR, R&D, Supply Chain
  3. `Super/Conscious AI` (conscious AI)
      - AI with human level consciousness
      - Requires self-awareness
      - Ex: Healthcare, autonomous vehicles, robotics, Natural Language Understanding
- `Breadth`: 
- `Applications`: 

### <a name='FundamentalApproachesToAI'></a>Fundamental Approaches to AI
- `Discriminative AI`: Approach that learns to distinguish between different classes of data, best for classification task and cannot understand context or generate new content.
- `Generative AI`: Generates new content based on training data, i


### <a name='Augmented-intelligence'></a>Augmented Intelligence
- Combines human strengths with machine intelligence.
- Uses AI to help us see and understand the world in new ways.
- Enables humans to accomplish things impossible alone.

### <a name='BranchesOfAi'></a>Branches of AI
[🔝](#table-of-contents)

- **Cognitive Computing**
  - Focuses on creating systems that simulate/mimic human thought processes
  - Involves intellectual activities like
      - Thinking
      - Reasoning
      - Problem-Solving
  - Core Elements of Cognitive Computing
      - `Perception`: Involves gathering and interpreting data from various sources to understand the environment.
      - `Learning`: Utilizes machine learning algorithms to analyze data and extract meaningful insights, improving over time.
      - Reasoning: Making accurate predictions and decisions based on data analytics.
      - `Reasoning`:

- **Machine Learning**
  - Subset of AI that analyzes data using computer algorithms and makes intelligent decisions based on its learning without being explicitly programmed.
  - Are
      - Trained with large data sets
      - Learns from examples, not rules
      - Enables machine to solve problems independently
      - Makes accurate predictions using given data

- **Deep Learning**
  - Specialized subset of machine learning, and uses multi-layered neural network known as deep neural networks to analyze complex data and simulate human decision making.
  - It allows continuous improvement and learning. 
  - Enhances AI's natural language understanding by grasping context and intent.
  - `Neural Networks`: Computation model inspired by brain's neural structure, composed of interconnected layers, mainly 3 layers.
      - `Input Layer`: Receives data
      - `Hidden Layers`: Processes data through multiple layers
      - `Output Layer`: Produces results

- **Generative AI**
  [💉](#generative-ai)
  - Generative AI refers to a class of artificial intelligence technologies that enable machines to autonomously create new content.
 
- **Natural Language Processing**
  - Subset of AI that enables computers to comprehend, interpret, and produce natural language.
  - NLP translates unstructured text into structured data and it involves two main components:
      - `Natural Language Understanding (NLU)` for converting unstructured to structured data.
      - `Natural Language Generation (NLG)` for the reverse.
  - Subcategories:
      - `Speech-to-Text`
      - `Text-to-Speech`

- **Computer Vision**
  - Field of AI which interprets and comprehends visual data, analyzes picture or video data to derive conclusions.
  - Applications:
      - `Image Classification`
      - `Object Detection`
      - `Image Segmentation Techniques`

### <a name='AiAigents'></a>AI Agents
- AI agents are software programs that autonomously interact with their environment, process data, and perform tasks to achieve human-defined goals.

### <a name='Robotics'></a>Robotics
- Involves designing, constructing and operating robots
- Made up of components:
    - `Sensors`: Acts as robot's eye and ears, gathers informations, detect obstacles
    - `Actutator`: Acts as robot's muscles, enables movement and interaction. Includes motos, hydraulic etc
    - `Controllers`: Acts as robot's brain, runs the software that control the robot parts and interpret sensor data
- `Cobots`: Robots that collaborate with humans using advanced sensors and AI technologies, communicate and coordinate actions which require teamwork.

### <a name='Prompts'></a>Prompts
[💉](#PromptEngineering)
- Prompt is any input or series of instructions used to produce a desired output, and help in directing the creativity of generative model.
- Building blocks of well structured prompt include:
    - Instruction
    - Context
    - Input Data
    - Output Indicators


## <a name='Brief'></a>Brief
[🔝](#table-of-contents)

### <a name='GenerativeAi'></a>Generative AI
- Generative AI refers to a class of artificial intelligence technologies that enable machines to autonomously create new content.
- `Language Models`
    - GPT Models: Used for text generation (e.g., ChatGPT).
    - Palm Models: Focused on text-in and out workflows.
    - Gemini Models: Multimodal capabilities, including text and image processing.
- `Image Generation Models`
    - Stable Diffusion: Advanced text-to-image technology.
    - DAL-E Model: Generates images that match input text.
    - StyleGAN: Produces high-quality images of faces and objects.
    - Super Resolution: Enhances image resolution by increasing pixel count.
- `Voice and Music Generation Models`
    - Murph: AI voice generation technology that replicates human speech nuances.
    - OpenAI Whisper: Transcription and translation model.
    - Jukedeck and Amper Music: AI-powered music generators for original tracks.
    - AIVA: Generates songs in various styles.
- `Video Generation Models`
    - Google's Imogen Video: Generates high-definition videos.
    - OpenAI Sora: Creates realistic scenes from text instructions.
- **Generative AI Models**
  - Generative AI models are AI systems that learn patterns from large datasets to create new content such as text, images, music, or video. Their design varies based on the task and data type.

  - Common types include (How does GenAI develop creativity?):
    - `VAEs (Variational Autoencoders)`: Encode input data into a latent space and decode it to generate new outputs. Used for image generation and anomaly detection (e.g., Fashion MNIST clothing images).
    - `GANs (Generative Adversarial Networks)`: Two networks (generator and discriminator) compete, improving each other. Used for image synthesis and style transfer (e.g., Nvidia's StyleGAN for realistic faces).
    - `Autoregressive Models`: Generate data step-by-step, using previous outputs as context. Useful for text and audio (e.g., WaveNet for speech).
    - `Transformers`: Use encoder-decoder layers for tasks like text generation and translation (e.g., GPT, Gemini).

    Models can be:
    - `Unimodal`: Input and output are the same type (e.g., GPT-3: text-to-text).
    - `Multimodal`: Handle multiple data types (e.g., DALL-E: text-to-image; ImageBind: combines text, audio, visuals).
- ****

### <a name='PromptEngineering'></a>Prompt Engineering
- Process of designing effective prompts to leverage the full capabilities of generative AI models and producing optimal responses.
- `Importance of Prompt Engineering`:
    - Optimizing model efficiency
    - Boosting performance for specific task
    - Understanding model constraints
    - Enhancing model security
- `Best Practices for Prompt Creation`:
    - **Clarity**: Use clear and concise language, avoid jargon and complex terms, and provide explicit instructions.
    - **Context**: Establish the context, provide relevant information.
    - **Precision**: Be specific and use examples.
    - **Role-Play/Persona Pattern**: Assume a persona, and provide context for role-play.
- `Prompt Engineering Tools`:
    - **IBM watsonx.ai Prompt Lab**
    - **Spellbook**: IDE by ScaleAI
    - **Dust**: WebInterface, Supports API intergation with other models and services
    - **PromptPerfect**: Optimize prompts for different LLMs for text and image models, supports GPT, Claude, StableLM, Llama, DALL-E, Stable Diffusion
    - **prompt-engineering (github)**
    - **OpenAI Playground**
    - **LangChain**: Python library with functionalities for building and chaining prompts.
    - **PromptBase**: Prompt's marketplace
- `Text-to-Text Prompt Techniques`: 
    - Task Specification
    - Contextual Guidance
    - Domain Expertise
    - Bias Mitigation
    - Framing
    - User Feedback Loop
    - **Zero-Shot Techniques**: Zero-shot prompting refers to the capability of LLMs to generate meaningful responses to prompts without needing prior training.
    - **Few-Shot Techniques**: Few-shot prompting used with LLMs relies on in-context learning. In this technique, demonstrations are provided in the prompt to steer the model toward better performance.
- `Common Useful Patterns`:
    - **Persona Pattern**: A technique where you instruct the AI to assume a specific role, expertise, or personality to provide more targeted and contextual responses. This helps the model adopt the knowledge, tone, and perspective of the specified persona, leading to more relevant and specialized outputs.
        ```
        You are an expert software architect with 15 years of experience in designing scalable systems. Provide recommendations for...
        ```
    - **Interview Pattern**: A method where you set up the AI as an interviewer who asks clarifying questions to gather necessary information before providing a comprehensive response. This ensures all relevant details are collected for optimal output generation.
        ```
        You will act as a SEO and content marketing expert. You will interview me, asking me (one at the time) all the relevant questions necessary for you to generate the best possible answer to my queries.
        ```
- `Chain-of-Thought approach`: Approach to solve complex problems by breaking them down into smaller, easier steps. 
    - **Few-Shot chain-of-thought**: Provides examples to break down problems.
    - **Zero-Shot chain-of-thought**: Encourages model to think on its own.
- `Tree-of-Though approach`: Prompting strategy designed to enhance the reasoning abilities of large language models by structuring thinking as a tree-like process. Instead of generating a single linear response, the model is encouraged to explore multiple reasoning paths, evaluate them, and select the most promising one. This allows for more deliberate and interpretable decision-making, especially in complex or open-ended tasks. *It allows the model to explore and evaluate multiple reasoning branches before deciding.*
    ```
    You are planning a school fundraising event.
    Follow this structure:

    List three different types of events (label them A, B, C).

    For each event, list:
        a. Key benefits
        b. Likely challenges
        c. What resources would be needed

    Compare the three events and choose the most feasible one. Explain why it is better than the others.
    ```
- `The Playoff Method`: The Playoff Method is a strategy used to compare responses generated from multiple prompts. The idea is to generate several different prompts for a given task, then compare the responses from each prompt through a pairwise comparison to determine which prompt results in the best output
    ```
    //Step1
    Can you provide me with 5 different text prompts, asking to generate a social media post celebrating NeoTech Solutions’ 100th enterprise software deployment? Also generate their possible responses. Keep it professional and concise (under 100 words). 

    Include the following elements: 
    1. Thanking the team 
    2. Highlighting innovation

    //Step2
    For each set of responses, perform a detailed pairwise comparison between every possible pair based on the following criteria: clarity of expression, coverage of the requirements, and engagement potential. Clearly state which response is stronger in each comparison, and then determine the overall strongest response by aggregating these pairwise results.

    Example:
    1. Compare Response 1 vs Response 2, noting which is clearer, more comprehensive, and more engaging.
    2. Repeat for Response 1 vs Response 3, Response 1 vs Response 4, and so on for all pairs.
    3. Summarize which responses perform best overall based on these pairwise assessments.
    ```
- `Text-to-Image Prompt Techniques`:
    - **Style Modifiers**: Keywords that define artistic style, medium, or visual aesthetic (e.g., "oil painting," "photorealistic," "anime style," "vintage," "cyberpunk").
    - **Quality Boosters**: Terms that enhance image quality and detail (e.g., "high resolution," "4K," "detailed," "sharp focus," "professional photography").
    - **Repetition**: Repeating key words or phrases to emphasize specific elements and increase their prominence in the generated image.
    - **Negative Prompts**: Specifying what NOT to include using terms like "no," "avoid," "exclude" to prevent unwanted elements (e.g., "no text," "no blur," "no distortion").
    - **Fix Deformed Generations**: Techniques to correct common AI generation issues like extra limbs, distorted faces, or unrealistic proportions using specific corrective terms.
- `Prompt Hacking`:
    - **Definition**: Techniques used to manipulate AI models to bypass safety measures, access restricted information, or generate content that violates intended use policies.
    - **Key Differences from Prompt Engineering**:
        - *Prompt Engineering*: Focuses on optimizing legitimate use cases and improving model performance for intended tasks
        - *Prompt Hacking*: Attempts to exploit model vulnerabilities and bypass safety constraints
    - **Common Techniques**:
        - *Jailbreaking*: Using creative prompts to make the model ignore safety instructions
        - *Role Playing*: Making the model assume a character that can perform restricted actions
        - *Indirect Prompting*: Asking for information in roundabout ways to avoid direct restrictions
        - *Context Manipulation*: Providing misleading context to trick the model
    - **Security Implications**: Understanding prompt hacking helps in developing better safety measures and robust AI systems

## <a name='Keyconcepts'></a>Key Concepts
[🔝](#table-of-contents)

## <a name='Popularalgorithms'></a>Popular Algorithms
[🔝](#table-of-contents)

## <a name='Toolsandlibraries'></a>Tools and Libraries
[🔝](#table-of-contents)

## <a name='References'></a>References
[🔝](#table-of-contents)
