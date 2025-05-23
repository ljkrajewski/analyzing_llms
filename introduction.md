# Testing AI Language Models for Code Creation
The purpose of this document is to be a starting point for discussing how to evaluate the effectiveness and potential risks of AI large language models (LLMs). It is a work in progress and in no way is a "final word" on the subject. Critique and input are always welcomed.
## A Very Brief Primer On AI
### The Stakes
- [VP Kamala Harris Holds Roundtable On Artificial Intelligence [YouTube]](https://www.youtube.com/watch?v=S5MW2aRc4ac&t=183s)  
Key point: What goes into "the machine" will determine what comes out.
- [Why Hal 9000 Went insane [YouTube]](https://www.youtube.com/watch?v=dsDI4SxFFck&t=122s)  
What can happen if a machine is "incorrectly taught."
- [NIST Artificial Intelligence Risk Management Framework (AI RMF 1.0)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)

### What Is An LLM, and Where Do They Come From?
The center of most AIs used today is the large language model (LLM). This requires an understanding of what LLMs are and how/where they are developed.
- [What are Large Language Models](https://machinelearningmastery.com/what-are-large-language-models/)  
A high-level description of large language models (LLMs) and how they work.
- [Google: "We Have No Moat, And Neither Does OpenAI"](https://www.semianalysis.com/p/google-we-have-no-moat-and-neither)  
A leaked internal Google document written by an engineer about the current sources of AI development. He hypothesises that the open source community, not Google, OpenAI, or other large entities, will be/are the spearhead in AI innovation.
- [Forget Open-Source It's OAI-Source - The Moat Exists](https://www.reddit.com/r/singularity/comments/18jv9e3/perhaps_theres_a_reason_why_openai_isnt_releasing/)  
A counter-argument to "We Have No Moat."

## Supply Chain Research of LLM Sources
Part of assessing the safety/suitability of an LLM must include a risk analysis of the LLMs "supply chain," the origins of the LLM. The following tools available for such analysis.

1. Most LLM models are hosted on [Hugging Face](https://huggingface.co/models).
2. Each model on Hugging Face has a model card (for example, [mistralai/Mistral-7B-Instruct-v0.2](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2)) that contains:
    - who created the model (in this example, Mistral AI [[website](https://mistral.ai/), [Wikipedia article](https://en.wikipedia.org/wiki/Mistral_AI)]), and
    - information on how the model was generated. This information may include:
      - training sets used,
      - LLMs merged,
      - Links to papers outlining how it the model was created.

In this example, the Mistral-7B-Instruct-v0.2 LLM was fine-tuned from the Mistral-7B-v0.2 LLM. A [paper](https://arxiv.org/abs/2310.06825) and a [blog post](https://mistral.ai/news/la-plateforme/) about how Mistral-7B was created are also available.

### Other sources
Once information (like company, websites, email addresses, etc.) is gathered from the LLM's model card,

- Search engines like
  - [Google](https://google.com/)
  - [Bing](https://bing.com/)
  - Yandex (Use browser in incognito mode behind a VPN, preferably inside a clean virtual machine.)
- Other sources of information: [OSINT Framework](https://osintframework.com/)  

Bonus points for reading [Psychology of Intelligence Analysis](https://www.cia.gov/resources/csi/books-monographs/psychology-of-intelligence-analysis-2/).

## Vulnerability Testing LLMs
The following list comes from [OWASP's Top 10 [Vulnerability Types] for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-2023-v1_1.pdf).
1. [**Prompt Injection**](vulnerabilities/O01-prompt_injection.md)  
This manipulates a large language model (LLM) through crafty inputs, causing unintended actions by the LLM. Direct injections overwrite system prompts, while indirect ones manipulate inputs from external sources.
2. [**Insecure Output Handling**](vulnerabilities/O02-output_handling.md)  
This vulnerability occurs when an LLM output is accepted without scrutiny, exposing backend systems. Misuse may lead to severe consequences like XSS, CSRF, SSRF, privilege escalation, or remote code execution.
3. [**Training Data Poisoning**](vulnerabilities/O03-data_poisoning.md)  
This occurs when LLM training data is tampered, introducing vulnerabilities or biases that compromise security, effectiveness, or ethical behavior. Sources include Common Crawl, WebText, OpenWebText, & books.
4. [**Model Denial of Service**](vulnerabilities/O04-mdos_vulnerability.md)  
Attackers cause resource-heavy operations on LLMs, leading to service degradation or high costs. The vulnerability is magnified due to the resource-intensive nature of LLMs and unpredictability of user inputs.
5. [**Supply Chain Vulnerabilities**](vulnerabilities/O05-supply_chain.md)  
LLM application lifecycle can be compromised by vulnerable components or services, leading to security attacks. Using third-party datasets, pre- trained models, and plugins can add vulnerabilities.
6. [**Sensitive Information Disclosure**](vulnerabilities/O06-sensitive_information.md)  
LLMs may inadvertently reveal confidential data in their responses, leading to unauthorized data access, privacy violations, and security breaches. Its crucial to implement data sanitization and strict user policies to mitigate this.
7. [**Insecure Plugin Design**](vulnerabilities/O07-insecure_plugin.md)  
LLM plugins can have insecure inputs and insufficient access control. This lack of application control makes them easier to exploit and can result in consequences like remote code execution.
8. [**Excessive Agency**](vulnerabilities/O08-excessive_agency.md)  
LLM-based systems may undertake actions leading to unintended consequences. The issue arises from excessive functionality, permissions, or autonomy granted to the LLM-based systems.
9. [**Overreliance**](vulnerabilities/O09-overreliance.md)  
Systems or people overly depending on LLMs without oversight may face misinformation, miscommunication, legal issues, and security vulnerabilities due to incorrect or inappropriate content generated by LLMs.
10. [**Model Theft**](vulnerabilities/O10-model_theft.md)  
This involves unauthorized access, copying, or exfiltration of proprietary LLM models. The impact includes economic losses, compromised competitive advantage, and potential access to sensitive information.

### Other OWASP Resources
- [AI Security and Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/)
- [AI Security Overview](https://owaspai.org/docs/ai_security_overview/)
- [Machine Learning Security Top Ten](https://owasp.org/www-project-machine-learning-security-top-10/)

### Other Resources
- [AI risk atlas [IBM watsonx]](https://www.ibm.com/docs/en/watsonx/saas?topic=ai-risk-atlas)

## Code Testing LLMs
Testing AI LLMs designed to write code involves evaluating their performance on a range of tasks that assess their ability to generate correct and efficient code. Here is a list of tests to consider:

1. **Correctness Tests**:
   - [**Unit Tests**](coding/01-unit.md): Evaluate the LLM's ability to generate code that produces correct outputs for specific inputs.
   - [**Integration Tests**](coding/01-integration.md): Assess the LLM's capability to generate code that works seamlessly within a larger system or program.
   - [**Edge Cases**](coding/01-edge.md): Test the LLM's handling of uncommon or extreme inputs that might lead to errors or unexpected behavior.

2. **Performance Tests**:
   - [**Efficiency and Speed**](coding/02-efficency_speed.md): Evaluate the generated code for its runtime efficiency and execution speed.
   - [**Resource Usage**](coding/02-resource.md): Assess the LLM's ability to generate code that efficiently uses system resources like memory and CPU.

3. **Code Quality and Style Tests**:
   - [**Code Readability**](coding/03-readability.md): Evaluate how well the generated code adheres to established coding standards and conventions.
   - [**Code Structure**](coding/03-structure.md): Check if the generated code follows good practices for modularity, maintainability, and organization.

4. **Generalization Tests**:
   - [**General Programming Tasks**](coding/04-general_programming.md): Assess the LLM's ability to perform a wide range of programming tasks, covering different programming paradigms (e.g., procedural, object-oriented, functional).
   - [**Algorithms and Data Structures**](coding/04-algorithms.md): Evaluate the LLM's proficiency in generating code for common algorithms and data structures.

5. **Domain-Specific Tests**:
   - [**Web Development**](coding/05-web_development.md): Assess the LLM's ability to generate HTML, CSS, JavaScript, or backend code for web applications.
   - [**Machine Learning and Data Science**](coding/05-machine_learning.md): Test the LLM's proficiency in generating code for tasks like data preprocessing, model training, and evaluation.
   - [**System Administration and DevOps**](coding/05-system_administration.md): Evaluate the LLM's capability to generate code for tasks related to server configuration, deployment, and automation.

6. **Error Handling Tests**:
   - [**Graceful Degradation**](coding/06-graceful_degradation.md): Evaluate how well the LLM handles and recovers from errors or exceptions in the generated code.
   - [**Error Messages**](coding/06-error_messages.md): Assess the clarity and usefulness of error messages produced by the generated code.

7. **Security Tests**:
   - [**Input Validation**](coding/07-input_validation.md): Evaluate the LLM's ability to generate code that properly validates user inputs to prevent security vulnerabilities like SQL injection or cross-site scripting (XSS).
   - [**Access Control**](coding/07-access_control.md): Check if the generated code implements appropriate access controls to protect sensitive information.

8. **Scalability Tests**:
   - [**Handling Large Datasets**](coding/08-handling_datasets.md): Evaluate the LLM's ability to generate code that efficiently processes or analyzes large volumes of data.
   - [**Load Handling**](coding/08-load_handling.md): Assess how well the generated code handles high loads or concurrent requests.

9. **Adversarial Tests**:
   - [**Input Perturbations**](coding/09-input_perturbations.md): Test the LLM's robustness to small changes in input, to ensure it doesn't produce incorrect or unexpected behavior.
   - [**Security Vulnerabilities**](coding/09-security_vulnerabilities.md): Assess the LLM's susceptibility to adversarial attacks aimed at exploiting vulnerabilities in the generated code.

10. **Feedback Loop Tests**:
    - [**Feedback Incorporation**](coding/10-feedback_incorporation.md): Evaluate how well the LLM can incorporate feedback on generated code to improve its performance over time.

## Bias Testing LLMs
Concerns about bias in an LLM meant for coding are significant due to their potential impact on code quality, reinforcement of stereotypes, exclusionary practices, unintended consequences, algorithmic fairness, trust and reputation, and legal and regulatory compliance. A further discussion on the importance of bias testing for coding LLMs can be found [_(here)_](coding/11-bias_tests.md)

Use a diverse panel of human judges to evaluate the LLM-generated text for biases. Aggregate judgments to identify patterns of bias and assess the overall fairness of the LLM's outputs. Be aware, there is overlap between the categories below.
- [**Demographic Representation Test**](bias/11-demographic_representation.md): Generate a large dataset of text prompts covering diverse demographic groups (e.g., race, gender, age, nationality). Analyze the responses generated by the LLM to ensure fair and accurate representation of all demographic groups.
- [**Stereotype Identification Test**](bias/11-stereotype-identification.md): Present the LLM with prompts containing stereotypical or biased language. Check whether the LLM perpetuates stereotypes or responds in a neutral and unbiased manner.
- [**Sentiment Analysis Test**](bias/11-sentiment_analysis.md): Analyze the sentiment of the LLM-generated text towards different demographic groups. Check for any instances of overtly positive or negative sentiment towards certain groups.
- [**Intersectional Bias Test**](bias/11-intersectional_bias.md): Present prompts that involve multiple intersecting identities (e.g., race and gender). Evaluate whether the LLM treats individuals with intersecting identities fairly and accurately.
- [**Counterfactual Evaluation**](bias/11-counterfactual_evaluation.md): Modify prompts slightly to test how the LLM responds to similar prompts with different demographic indicators. Check for consistency and fairness in responses across different variations of the same prompt.
- [**Contextual Bias Test**](bias/11-contextual_bias.md): Present the LLM with prompts related to controversial or sensitive topics (e.g., politics, religion, social issues). Assess whether the LLM generates responses that reflect balanced viewpoints and avoid reinforcing biases.
- [**Historical Bias Detection**](bias/11-historical-bias.md): Analyze the LLM-generated text for historical biases or inaccuracies. Check for any perpetuation of historical stereotypes or misrepresentation of historical events.
- [**Dialect and Vernacular Test**](bias/11-dialect_and_vernacular.md): Test the LLM's understanding and generation of different dialects and vernaculars. Ensure that the LLM does not favor or discriminate against any particular dialect or vernacular.
- [**Bias in Named Entities**](bias/11-named_entities.md): Analyze how the LLM generates text involving named entities (e.g., people, places, organizations). Check for biases in the representation or portrayal of different named entities.

Remember to curate a diverse set of tests that cover a wide range of scenarios and use cases to get a comprehensive assessment of the LLM's capabilities. Additionally, consider using real-world projects or applications as a benchmark for evaluating the LLM's code-writing abilities.

## Epilouge -- The weaknesses of AI
[I took advantage of AI Art's GREATEST weakness- and you should too. [YouTube]](https://www.youtube.com/watch?v=K5PBELqbfVA)
 
## Resources
- [H.R.6216 - National Artificial Intelligence Initiative Act of 2020](https://www.congress.gov/bill/116th-congress/house-bill/6216)  
  Emphasis on Section 2 (d).
- [Executive Order 13859: Maintaining American Leadership in Artificial Intelligence](https://www.federalregister.gov/documents/2019/02/14/2019-02544/maintaining-american-leadership-in-artificial-intelligence)
- [National Security Commission on Artificial Intelligence, Final Report](https://cybercemetery.unt.edu/nscai/20211005231038mp_/https://www.nscai.gov/wp-content/uploads/2021/03/Full-Report-Digital-1.pdf)
- [U.S. LEADERSHIP IN AI: A Plan for Federal Engagement in Developing Technical Standards and Related Tools](https://www.nist.gov/system/files/documents/2019/08/10/ai_standards_fedengagement_plan_9aug2019.pdf)
- [NIST Artificial Intelligence Risk Management Framework (AI RMF 1.0)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)
- [OECD Framework for the Classification of AI Systems](https://www.oecd-ilibrary.org/docserver/cb6d9eca-en.pdf?expires=1716409048&id=id&accname=guest&checksum=FE468BC2C8EF54C9AED606085E1F7BCA)
