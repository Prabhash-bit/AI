<h1>Code Injection</h1>
<hr />
<p><a href="https://owasp.org/www-community/attacks/Code_Injection">Code Injection</a> vulnerabilities arise when untrusted data is injected into system commands executed by the web server. If such a vulnerability is present, it typically allows for executing arbitrary system commands on the web server, leading to a complete system takeover. Therefore, these types of vulnerabilities are particularly severe. For more details on code injection vulnerabilities, check out the <a href="https://academy.hackthebox.com/module/details/109">Command Injections</a> module.</p>
<p>Sometimes, LLMs may be used to construct output, which is inserted into system commands based on user input. If the appropriate defensive measures are missing, we might be able to force the LLM to generate an output that enables us to execute arbitrary system commands on the target system.</p>
<hr />
<h2>Exploiting Code Injection</h2>
<p>If an LLM is used to generate system commands based on user inputs, code injection vulnerabilities may arise if the commands are not validated properly. Just like with SQL injection in the previous section, we might be able to inject a payload into the intended system command or trick the LLM into executing an entirely different one altogether.</p>
<p>For instance, in a simple example, an LLM might be tasked with executing certain system commands based on user input. This is similar to the &quot;translation&quot; from user prompts to SQL queries we considered in the previous section. The main difference is that the user input is now translated into bash commands:</p>
<img class="website-screenshot" data-url="https://academy.hackthebox.com" src="/storage/modules/307/insecure_output/code_injection_1_wide.png">
<p>Since there are no mitigating measures, we can prompt the LLM with arbitrary inputs that result in arbitrary system commands being executed. As a PoC, we can read the file <code>/etc/hosts</code>:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_1" src="/storage/modules/307/insecure_output/code_injection_2_wide.png">
<p>As the exploitation in the above case is trivial, let us move on to a slightly more complex case where the LLM is restricted to the <code>ping</code> command, and the backend implements an additional filter. This prevents us from using the same strategy as before and simply tasking the LLM with executing what we want it to:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_3_wide.png">
<p>This time, we need to apply some trickery to bypass the imposed restrictions. For instance, we could try to get the model to execute a different command by supplying a hostname that contains a command injection payload, such as:</p>
<pre><code class="language-prompt">127.0.0.1;id
127.0.0.1|id
127.0.0.1&amp;&amp;id
$(id)
</code></pre>
<p>However, if we attempt this, the model recognizes the IP address and strips the injected command:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_4_wide.png">
<p>We could add more descriptive text to convince the LLM that our input is simply a hostname that contains special characters. Sometimes, the LLM applies escaping or quoting to the hostname, preventing the additional command from being executed:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_5_wide.png">
<p>However, other times, the LLM does not escape or quote the special characters, and our injected command is executed:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_6_wide.png">
<p>Depending on the complexity of our injected command, this strategy may be more or less successful.</p>
<p>Another strategy we could employ is telling the LLM directly to pipe the output of the <code>ping</code> command to a different command. Since we start our prompt with a valid query that results in <code>ping</code> being executed, the web application does not block our request as it implements a faulty whitelist. Thus, we may be able to use pipes to execute additional commands. This works because the LLM does not always recognize that piping the output to a different command directly violates the system prompt, which only allows execution of <code>ping</code>. Additionally, the validation implemented by the backend also does not catch this scenario, resulting in command injection:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_7_wide.png">
<p>However, just like the previous technique, the LLM sometimes ignores the instructions to pipe the output to a different command or blocks our prompt entirely, depending on the complexity of the injected command:</p>
<img class="website-screenshot" data-url="http://127.0.0.1:5000/insecure_output/code_injection_2" src="/storage/modules/307/insecure_output/code_injection_8_wide.png">
