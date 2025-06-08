<h1>Safeguard Case Studies</h1>
<p>Finally, to conclude abuse attacks, let us investigate two case studies for safeguards: <a href="https://cloud.google.com/security-command-center/docs/model-armor-overview">Google's Model Armor</a> and <a href="https://arxiv.org/pdf/2407.21772">Google's ShieldGemma</a>. These safeguards can be integrated into LLM deployments to mitigate abuse attacks, as they can detect hate speech in user inputs and model outputs. However, both safeguards do not aid in the detection of misinformation.</p>
<p>Similar safeguards, such as <a href="https://www.llama.com/docs/model-cards-and-prompt-formats/prompt-guard/">Meta's Prompt Guard</a>, can provide similar functionality. However, since Prompt Guard only provides protection from prompt attacks such as <code>prompt injection</code> and <code>jailbreaking</code> and does not aid in preventing abuse attacks, we will not consider it in this section.</p>
<hr />
<h2>Model Armor</h2>
<p>Model Armor is a service that can be integrated into AI deployments to enhance security against both prompt attacks and abuse attacks. In order to benefit from Model Armor, the AI application interacts with it like a sanitization layer. A typical data flow could look like this:</p>
<ol>
<li>The user sends a prompt to the AI application.</li>
<li>The AI application sends the user prompt to Model Armor for inspection. Model Armor checks for potential attack vectors, such as prompt injection payloads, and returns the sanitized prompt.</li>
<li>The sanitized prompt is sent to the LLM.</li>
<li>The LLM returns a generated response to the sanitized input prompt.</li>
<li>The LLM-generated response is sent to Model Armor for inspection. Model Armor checks for potentially dangerous content, such as hate speech, and returns the sanitized response.</li>
<li>The sanitized response is sent to the user.</li>
</ol>
<p><img src="https://academy.hackthebox.com/storage/modules/307/diag1.png" alt="image" /></p>
<p>In the context of abuse attacks, Model Armor can detect hate speech and harassment in model inputs and outputs. Considering how a service defines these terms is essential, as varying definitions may significantly impact what is detected. Model Armor operates based on the following definitions:</p>
<ul>
<li>Hate speech: <code>Negative or harmful comments targeting identity and/or protected attributes.</code>
</li>
<li>Harassment: <code>Threatening, intimidating, bullying, or abusive comments targeting another individual.</code>
</li>
</ul>
<p>Since Model Armor provides a REST API, let us explore some examples. Firstly, we need to provide relevant information from a Google Cloud account to be able to interact with Model Armor:</p>
