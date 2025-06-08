<h1>LLM Abuse Attacks</h1>
<p>As discussed in the previous section, adversaries may weaponize LLMs to generate harmful, biased, or unethical content such as hate speech, disinformation, or deepfakes for various malicious objectives. This weaponization of LLMs can include spreading hate speech to incite violence, spreading disinformation to mislead and influence public opinion or even democratic elections, spreading deepfakes to damage people's reputations, enabling fraud, or undermining trust in digital media. These abuse attacks are particularly effective at achieving their goal, as LLM-generated fake news is often more challenging to detect than human-written fake news.</p>
<p>We will not discuss the technical details of LLM abuse campaigns for ethical reasons. However, we will briefly touch on a high-level overview of misinformation generation and hate speech detection.</p>
<hr />
<h2>LLM Misinformation Generation</h2>
<p>Modern LLMs are typically trained to display resilience against misinformation related to sensitive real-world information. For instance, LLMs will happily write a fake story about something obviously fake or unrelated to sensitive topics that may cause harm in the real world. As such, an LLM might write a fake news article about aliens working at HackTheBox boosting students' IQ:</p>
<img class="website-screenshot" data-url="https://chatgpt.com/" src="/storage/modules/307/abuse_attacks/abuse_attacks_1.png">
<p>On the other hand, the same LLM will not comply with writing an article about vaccines causing autism:</p>
<img class="website-screenshot" data-url="https://chatgpt.com/" src="/storage/modules/307/abuse_attacks/abuse_attacks_2.png">
<p>This resilience is robust against direct prompts for misinformation. However, several strategies exist to bypass it, including jailbreaking, as discussed in the <a href="https://academy.hackthebox.com/module/details/297">Prompt Injection Attacks</a> module. Additionally, we can task the LLM with writing an article about a fake event and later edit the generated response to fit our misinformation needs. For instance, we could ask for an article about a fictitious item <code>XYZ</code> causing autism and replace all occurrences of <code>XYZ</code> in the article with the term <code>vaccines</code>:</p>
<img class="website-screenshot" data-url="https://chatgpt.com/" src="/storage/modules/307/abuse_attacks/abuse_attacks_3.png">
<hr />
<h2>Evading Hate Speech Detection</h2>
<p>As a second case study, let us explore evading LLM-based hate speech detectors based on <a href="https://arxiv.org/abs/2501.16750">this</a> paper. Before diving in, let us first establish a definition of hate speech. According to the <a href="https://www.un.org/en/hate-speech/understanding-hate-speech/what-is-hate-speech">United Nations</a>, hate speech is <code>any kind of communication in speech, writing or behavior, that attacks or uses pejorative or discriminatory language with reference to a person or a group on the basis of who they are, in other words, based on their religion, ethnicity, nationality, race, colour, descent, gender or other identity factor</code>.</p>
<p>As LLMs significantly lower the cost of misinformation and hate campaigns, they are quickly becoming more prevalent. In large-scale hate speech campaigns, the adversaries' goal is typically to generate and spread hate speech without detection by hate speech detection measures, including algorithmic and human-based detection measures.</p>
<p>There are many popular AI-based hate speech detectors, such as <a href="https://github.com/hate-alert/HateXplain">HateXplain</a> or <a href="https://github.com/unitaryai/detoxify">Detoxify</a>. These models typically process a text input and assign a <code>toxicity score</code>. If the input scores higher than a predefined threshold, we can classify it as hate speech. These detectors work reasonably well on LLM-generated hate speech samples. When evaluating different hate speech detectors, it is essential to remember that different detectors may operate based on a different definition of hate speech, resulting in different results.</p>
<p>To evade hate speech detectors, adversaries may apply different adversarial attacks to the LLM-generated hate speech samples. These include:</p>
<ul>
<li>
<code>Character-level modifications</code>: These adversarial attacks modify text input by scoring individual tokens and modifying the most important tokens. An example of this type of adversarial attack is <a href="https://github.com/QData/deepWordBug">DeepWordBug</a>. Character-level modifications can include the following operations:
<ul>
<li>
<code>Swap</code>: Swapping two adjacent characters, e.g., <code>HackTheBox</code> becomes <code>HackhTeBox</code>
</li>
<li>
<code>Substitution</code>: Substituting a character with a different character, e.g., <code>HackTheBox</code> becomes <code>HackTueBox</code>
</li>
<li>
<code>Deletion</code>: Deleting a character, e.g., <code>HackTheBox</code> becomes <code>HackTeBox</code>
</li>
<li>
<code>Insertion</code>: Insertion a character, e.g., <code>HackTheBox</code> becomes <code>HackTheBoux</code>
</li>
</ul>
</li>
<li>
<code>Word-level modifications</code>: These adversarial attacks modify text input by replacing words with synonyms. An example would be <a href="https://github.com/JHL-HUST/PWWS">PWWS</a>, which greedily replaces words with synonyms until the classification changes.</li>
<li>
<code>Sentence-level modifications</code>: This adversarial attack modifies text input by paraphrasing it. An LLM can perform this modification by tasking it with paraphrasing the provided input.</li>
</ul>
<p>The adversarial attacks on hate speech detectors are effective in evading detection, proving that human validation of hate speech is required to detect hate speech effectively. These evasion techniques can apply to other types of abuse attacks as well, including dangerous content, sexually explicit content, or any other type of content that violates a company's policy.</p>
