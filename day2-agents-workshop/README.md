# AWS Deployment AI Agent

## 1. Use Case
**Problem**: Developers struggle with AWS deployment steps and terminology for Java apps.

**User**: Fullstack Java Developers.

**Goal**: A conversational AI assistant to explain AWS concepts using Wikipedia.

 #### Example User Inputs:

   * Suggest an instance type for a Java project.
   * What is AWS EC2?
   * What is Lambda in AWS?
   * How to deploy a java application on AWS?


## 2. LLM Choice
**Model** : Google Gemini Flash-Lite latest.

* The model was selected for its high-speed performance and low latency. In a DevOps context, developers need rapid responses for command-line queries. Gemini Flash-Lite provides a balance between technical reasoning and fast inference.
## 3. Tools Used
**Tool**: Wikipedia

* This tool fetches verified, real-time technical definitions. It ensures that when a user asks about complex infrastructure (e.g., "What is a AWS?"), the agent provides grounded, factual information rather than relying solely on internal training data.

## 4. Memory Used
**Node**: Simple Memory.

* This node retains the context of the last few interactions. This is critical for deployment tasks. For instance, if a user asks about a t2.micro instance, they can later ask, "How much RAM does it have?" without re-specifying the instance type.

## 5. Workflow Screenshot
**Workflow-images : **

<img width="1729" height="728" alt="image" src="https://github.com/user-attachments/assets/58b21714-a531-449f-a69a-5e4906386707" />

** Output-images : ** 
<img width="1860" height="894" alt="image" src="https://github.com/user-attachments/assets/41880be3-b7af-4f3d-b6bb-aa062df76b87" />


## 6. Reflection (Task 4)
**What does the agent do well?**
* The agent excels at breaking down complex AWS concepts into beginner-friendly steps and accurately uses external tools for definitions.

**Current limitations:**
* It is an informational agent and cannot yet execute live AWS CLI commands or modify real cloud infrastructure.

**Future Improvements:** 
*  Integrate the HTTP Request Tool to connect with AWS APIs to automate instance creation directly from the chat.

**Memory's Usefulness:** 
* Memory makes the assistant feel like a real peer. It remembers the specific Java environment discussed, saving the user from repetitive typing.

**Tool Behavior:**
* The Wikipedia tool worked seamlessly. An observed edge case was when a term had multiple meanings; however, the system prompt helped keep the context focused on DevOps.

## 7. Core Concept Questions

### 1.Difference between a simple LLM call and an LLM-powered agent?

* An LLM call is a single prediction based on a prompt. An Agent uses the LLM as a reasoning core to decide which tools to use and how to execute multi-step tasks autonomously.

### 2.Role of the system prompt?
* The system prompt defines the agent's identity (like: DevOps Specialist) sets its tone, and provides instructions on how to prioritize tool use and handle specific user queries.
  
### 3.How does tool use extend LLM capabilities?
* Tools allow the LLM to access live data, perform math, or interact with external software, providing information and actions that were not available in its static training dataset.
### 4.Trade-offs between short-term (window buffer) and long-term (database) memory?

* Window buffer memory is fast and easy to implement for single sessions but loses data once the limit is reached. Database memory is persistent and scales for long-term user history but requires more setup.

### 5.Purpose of the AI Agent node in n8n vs. an LLM Chain node?
* The AI Agent node is "loopy" and autonomous, it decides the path to the solution. An LLM Chain follows a fixed, linear sequence of steps defined by the developer.

### 6.Risks or failure modes observed?
* One primary risk observed was response delay when the agent was deciding whether to use a tool or not. Also, there is a risk of outdated information, as the agent depends on Wikipedia which might not always have the very latest AWS feature updates. Lastly, if the API connection fails, the agent becomes unresponsive, which is a critical failure mode in a real production environment.

### 7.How to evaluate agent performance in production?
* Evaluation should be based on Accuracy (correctness of technical advice), Latency (response speed), and User Completion Rate (how often the user successfully finishes a task).



