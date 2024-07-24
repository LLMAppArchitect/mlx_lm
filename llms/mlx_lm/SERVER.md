# HTTP Model Server

You use `mlx-lm` to make an HTTP API for generating text with any supported
model. The HTTP API is intended to be similar to the [OpenAI chat
API](https://platform.openai.com/docs/api-reference).

> [!NOTE]  
> The MLX LM server is not recommended for production as it only implements
> basic security checks.

Start the server with:

```shell
mlx_lm.server --model <path_to_model_or_hf_repo>
```

For example:

```shell
mlx_lm.server --model mlx-community/Mistral-7B-Instruct-v0.3-4bit --trust-remote-code --port 8722

mlx_lm.server --model mlx-community/Mistral-Nemo-Instruct-2407-8bit --trust-remote-code --port 8723

mlx_lm.server --model mlx-community/internlm2_5-7b-chat-8bit --trust-remote-code --port 8722
```

This will start a text generation server on port `8080` of the `localhost`
using Mistral 7B instruct. The model will be downloaded from the provided
Hugging Face repo if it is not already in the local cache.

To see a full list of options run:

```shell
mlx_lm.server --help
```

You can make a request to the model by running:

```shell
curl localhost:8722/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
     "messages": [{"role": "user", "content": "Say this is a test!"}],
     "temperature": 0.7,
     "max_tokens": 100,
   }'
```

output:

```json 
{
  "id": "chatcmpl-74e66064-8727-411a-ada3-d5287b2c83a2",
  "system_fingerprint": "fp_73a731bd-bd00-4dcd-8fac-8f3f452210a2",
  "object": "chat.completions",
  "model": "default_model",
  "created": 1721634359,
  "choices": [
    {
      "index": 0,
      "logprobs": {
        "token_logprobs": [
          -2.4453125,
          -1.28125,
          -1.421875,
          -0.25,
          -7.53125,
          -1.15625,
          -4.09375,
          -0.390625,
          -3.0625,
          -0.84375,
          -2.53125,
          -0.125,
          -0.40625,
          -0.015625,
          -0.15625,
          -0.265625,
          -1.015625,
          -1.6484375,
          -1.0625,
          -0.40625,
          -4.390625,
          -0.296875,
          -1.078125,
          -3.0625,
          -0.328125,
          -0.21875,
          -0.390625,
          -2.015625,
          -3.46875,
          0.0,
          -0.765625,
          -2.609375,
          -1.921875,
          -1.078125,
          -1.859375,
          -1.625,
          -0.09375,
          -0.015625,
          -1.5625,
          -2.1015625,
          -1.65625,
          -0.21875,
          0.0,
          0.0,
          -1.640625,
          -0.0625,
          0.0,
          -1.234375,
          -0.6875,
          -0.53125,
          -0.078125,
          -0.03125,
          -1.015625,
          -0.109375,
          -3.4765625,
          -0.015625,
          -2.140625,
          -1.34375,
          -1.0625,
          -2.21875,
          -1.046875,
          -0.046875,
          -0.375,
          -1.0,
          -1.0625,
          -3.21875,
          -0.5,
          -0.234375,
          -0.15625,
          -2.015625,
          -1.265625,
          -0.390625,
          -2.265625,
          -0.0625,
          -1.59375,
          -3.5625,
          -0.59375,
          -0.46875,
          -1.0,
          -1.3515625,
          -0.296875,
          -1.4375,
          0.0,
          -1.1875,
          -0.46875,
          -0.15625,
          -0.375,
          -0.0625,
          -0.0625,
          -3.90625,
          -0.9375,
          -0.5625,
          -0.25,
          -2.53125,
          -0.28125,
          -2.640625,
          -0.59375,
          -0.75,
          -0.53125,
          -0.71875
        ],
        "top_logprobs": [],
        "tokens": [
          39584,
          346,
          5846,
          725,
          3716,
          489,
          4330,
          25341,
          16375,
          3103,
          1226,
          725,
          395,
          3556,
          1593,
          43916,
          465,
          2423,
          57436,
          334,
          19109,
          446,
          395,
          16375,
          22006,
          55098,
          465,
          53057,
          51040,
          334,
          465,
          848,
          285,
          3235,
          53057,
          4144,
          334,
          465,
          461,
          2423,
          57436,
          830,
          285,
          3235,
          5168,
          334,
          465,
          461,
          2136,
          505,
          395,
          1420,
          17338,
          465,
          312,
          281,
          5128,
          285,
          2423,
          5128,
          1883,
          938,
          334,
          55098,
          10363,
          6069,
          410,
          1420,
          328,
          410,
          2863,
          46301,
          2119,
          517,
          2014,
          334,
          4872,
          285,
          3235,
          2423,
          11740,
          334,
          465,
          29581,
          560,
          410,
          1420,
          4736,
          505,
          6662,
          12590,
          281,
          1239,
          1377,
          3089,
          22865,
          560,
          810,
          6025,
          3328
        ]
      },
      "finish_reason": "length",
      "message": {
        "role": "assistant",
        "content": "Sure! Here's What I'd Say Given That It's a Test:\n\n---\n\n**Test Scenario: Validation of a Given Statement**\n\n**Scenario Outline:** \n- **Scenario Name:** \"Test Scenario\"\n- **Description:** \"This is a test!\"\n\n**1. Pre-Test Preparations:**\n\nBefore starting the test, the following preparations must be made: \n\n- **Test Environment:** Ensure that the test environment is setup correctly. This may include ensuring that all necessary software"
      }
    }
  ],
  "usage": {
    "prompt_tokens": 16,
    "completion_tokens": 100,
    "total_tokens": 116
  }
}

```

### Request Fields

- `messages`: An array of message objects representing the conversation
  history. Each message object should have a role (e.g. user, assistant) and
  content (the message text).

- `role_mapping`: (Optional) A dictionary to customize the role prefixes in
  the generated prompt. If not provided, the default mappings are used.

- `stop`: (Optional) An array of strings or a single string. Thesse are
  sequences of tokens on which the generation should stop.

- `max_tokens`: (Optional) An integer specifying the maximum number of tokens
  to generate. Defaults to `100`.

- `stream`: (Optional) A boolean indicating if the response should be
  streamed. If true, responses are sent as they are generated. Defaults to
  false.

- `temperature`: (Optional) A float specifying the sampling temperature.
  Defaults to `1.0`.

- `top_p`: (Optional) A float specifying the nucleus sampling parameter.
  Defaults to `1.0`.

- `repetition_penalty`: (Optional) Applies a penalty to repeated tokens.
  Defaults to `1.0`.

- `repetition_context_size`: (Optional) The size of the context window for
  applying repetition penalty. Defaults to `20`.

- `logit_bias`: (Optional) A dictionary mapping token IDs to their bias
  values. Defaults to `None`.

- `logprobs`: (Optional) An integer specifying the number of top tokens and
  corresponding log probabilities to return for each output in the generated
  sequence. If set, this can be any value between 1 and 10, inclusive.
