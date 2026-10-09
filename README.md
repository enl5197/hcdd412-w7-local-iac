AI USED: Copilot, Chatgpt 

Link to Repo: https://github.com/enl5197/hcdd412-w7-local-iac.git 

Reflection: 
The prompt I used to generate the docker compose file was: " Write a Docker Compose file (compose.yaml) with an nginx web service and an Ollama AI service on one network. Take the web port, AI port, environment name and web memory limit from environment variables, and fail with a clear message if the port or environment name is missing. Add a healthcheck for nginx, labels with the environment name, a named volume for Ollamamodels, and pin image tags. No secrets in the file.” Which was the same prompt that was in the lab guide. When it was generating the compose.yaml file it only prompted me to accept the final file, which I did after looking over it. Overall, the compose.yaml file was correct and I did not have to make any changes. To validate I used: docker compose -p hcdd412-dev --env-file dev.env config. I did run into some errors the first time I used the command because I did not realize I have to save any changes I make to the file before running a command or else I would get an error. I ran into this issue on multiple occasions, but it made me realize the importance of saving code after every step in case my computer crashes or I get disconnected, that way all my code is preserved.  

Part 6 Analysis

Experiment 3 changed the memory limit of a running container then asked Compose to converge it back to its original amount. Experiment 4 created a snowflake manually to see if Compose was aware it existed. Compose did not know about it because it was outside of its view. Path A's preview shows the infrastructure of the cloud concept whereas Compose does not provide the same level of visibility. This connects to the AWS outage reading and to configuration drift because when manual changes are untracked and the IaC is not updated, an application's settings could drift away from the baseline.  


AI Service Proof of Concept

PS C:\Users\enwat\Documents\hcdd412-w7-local-iac> Invoke-RestMethod -Uri http://localhost:11434/api/generate -Method Post -Body $body -ContentType "application/json"


model                    : llama3.2:1b
created_at               : 2026-10-09T21:05:17.346054481Z
response                 : Positive
done                     : True
done_reason              : stop
context                  : {128006, 9125, 128007, 271...}
total_duration           : 5118802001
load_duration            : 4503185848
prompt_eval_count        : 53
prompt_eval_cached_count : 0
prompt_eval_duration     : 565043000
eval_count               : 2
eval_duration            : 35580000

This component would sit behind your Week 6 inference boundary where external apps can interact with OLLAMA without exposing it to the user interface. The small model's answer was correct 