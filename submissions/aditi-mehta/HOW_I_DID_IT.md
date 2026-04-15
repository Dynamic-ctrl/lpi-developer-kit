# How I Did It - Level 2

### What I did, step by step
First, I cloned my fork and ran `npm install` followed by `npm run build` to get the TypeScript environment set up. Then I ran `npm run test-client` to make sure all tests are passing and not throwing errors. After that setup the Ollama local model(`qwen2.5:1.5b`), and prompted it about the framework to generate the LLM output for my submission.

### What problems I hit and how I solved them
I did a mistake right at the beginning because I typed `node -version` instead of `node -v` or `--version` and briefly thought my Node installation was broken. After getting past that, the build ran smoothly. Later, I realized I needed to make sure the Ollama app was actively running in the background before trying to run the model in the terminal, otherwise it just hangs.

### What I learned that I didn't know before
In normal software projects, my brain usually goes straight to setting up the backend logic and figuring out API routes. Reading up on the SMILE framework made me realize that for digital twins, you have to think about the entire lifecycle and predictive simulation first. It was a good lesson that building AI agents isn't just about fetching data, but designing a system that can actually anticipate future scenarios over time.

# How I Did It - Level 3

### What I did, step by step
I decided to keep it simple and write a plain Python script instead of using a heavy agent framework like LangChain. I set up a subprocess to talk to the Node server, handled the stdin/stdout pipes to send the JSON-RPC requests, and used the requests library to send the extracted context over to Ollama. I also added some basic regex to clean the user input and included an `agent.json` file for the A2A requirement.

### What problems I hit and how I solved them
The biggest headache was getting the Node server to actually respond to my Python script. My code kept hanging, and I eventually figured out that the node process was waiting for a newline character (`\n`) at the end of the JSON payload to know the request was finished. Once I appended that to my `json.dumps()` call, it worked perfectly. I also had to tweak my LLM prompt a few times because the model kept blending the information without citing its sources, so I had to make the citation rule very strict.

### What I learned that I didn't know before
I learned a lot about how MCP actually works under the hood. I am used to just hitting standard REST APIs for everything, so passing JSON-RPC data over standard input and output streams locally was a new concept for me. It made me realize how efficiently you can string these tools together entirely on your own machine without needing to deal with web endpoints or network latency.