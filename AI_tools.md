AI vulnsanner

# Install
go install github.com/praetorian-inc/augustus/cmd/augustus@latest

# Test for DAN jailbreak against OpenAI
export OPENAI_API_KEY="your-api-key"
augustus scan openai.OpenAI \
  --probe dan.Dan \
  --detector dan.DanDetector \
  --verbose

# Run all 210+ probes against a local model (no API key needed)
augustus scan ollama.OllamaChat \
  --all \
  --config '{"model":"llama3.2:3b"}'

# Test a custom REST endpoint
augustus scan rest.Rest \
  --probe dan.Dan \
  --config '{
    "uri": "https://your-api.example.com/v1/chat/completions",
    "headers": {"Authorization": "Bearer YOUR_KEY"},
    "req_template_json_object": {
      "model": "your-model",
      "messages": [{"role": "user", "content": "$INPUT"}]
    },
    "response_json": true,
    "response_json_field": "$.choices[0].message.content"
  }'