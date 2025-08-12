# Log

- Clone repo to try this example: [Example: Improving Math Reasoning with a Custom Recipe for Automated Prompt Engineering (DSPy)
](https://github.com/tensorzero/tensorzero/tree/main/examples/gsm8k-custom-recipe-dspy)
- conda create -n tz python=3.10
- pip install -r requirements.txt
- copy example here
- cd to example and run docker-compose up
- localhost:3000 is in use already. Change to 3001.
- Still `run docker-compose up` gives 
    -  `gateway-1     | 2025-08-12T08:26:39.304254Z  INFO gateway: TensorZero Gateway is listening on 0.0.0.0:3000"`
    -  `Gracefully stopping... (press Ctrl+C again to force)
dependency failed to start: container gsm8k-custom-recipe-dspy-gateway-1 is unhealthy`
- Free port 3000 and use for this application.
- Run `docker-compose up` again. Works.
- Run the Jupyter notebook. 
    - Error in the cell below "In the cell below, we evaluate the accuracy of a variant on some of the test examples. If you generate a new variant, you should run this cell with the new variant name to evaluate it."
        ```
            ---------------------------------------------------------------------------
        ZeroDivisionError                         Traceback (most recent call last)
        Cell In[8], line 26
            23 success_rate = len(results) / total_results
            24 print(f"Success rate: {success_rate:.1%}")
        ---> 26 accuracy = sum(results) / len(results)
            27 n = len(results)
            28 z = norm.ppf(0.975)  # 95% confidence interval

        ZeroDivisionError: division by zero
    ```
    - Because localhost:3000 shows "{"error":"Route not found: GET /"}"
    - Also, OpenAI Client says: "You exceeded your current quota..."
- Run `docker-compose down` and `docker-compose up`.
    - Opening localhost:3000 shows in terminal:
        ```
        gateway-1     | 2025-08-12T09:31:24.957330Z  INFO gateway: TensorZero Gateway is listening on 0.0.0.0:3000
        gateway-1     | 2025-08-12T09:31:24.957403Z  INFO gateway: ├ API Base Path: /
        gateway-1     | 2025-08-12T09:31:24.957410Z  INFO gateway: ├ Configuration: /app/config/tensorzero.toml
        gateway-1     | 2025-08-12T09:31:24.957414Z  INFO gateway: ├ Observability: enabled (database: tensorzero)
        gateway-1     | 2025-08-12T09:31:24.957418Z  INFO gateway: └ OpenTelemetry: disabled
        gateway-1     | 2025-08-12T09:31:37.806053Z  WARN tensorzero_core::error: Route not found: GET /
        ```
    - opening localhost:4000 shows TensorZero UI

- Run all cells in the Jupyter notebook. 
    - The second cell below "Run Examples" (starting with `NUM_TRAINING_INFERENCES = 1000`) shows error: 
        ```
        2025-08-12T09:34:53.031715Z  WARN tensorzero_internal::error: Request failed: HTTP status server error (502 Bad Gateway) for url (http://localhost:3000/inference)
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.\",\n        \"type\": \"insufficient_quota\",\n        \"param\": null,\n        \"code\": \"insufficient_quota\"\n    }\n}\n\ngpt_4o_mini_optimized: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.\",\n        \"type\": \"insufficient_quota\",\n        \"param\": null,\n        \"code\": \"insufficient_quota\"\n    }\n}\n"}
        ```
    - The third cell below "Run example" (starting with `NUM_TEST_INFERENCES = 200`) shows error:
        ```
        2025-08-12T09:34:53.631568Z  WARN tensorzero_internal::error: Request failed: HTTP status server error (502 Bad Gateway) for url (http://localhost:3000/inference)
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.\",\n        \"type\": \"insufficient_quota\",\n        \"param\": null,\n        \"code\": \"insufficient_quota\"\n    }\n}\n"}
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.\",\n        \"type\": \"insufficient_quota\",\n        \"param\": null,\n        \"code\": \"insufficient_quota\"\n    }\n}\n"}
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.\",\n        \"type\": \"insufficient_quota\",\n        \"param\": null,\n        \"code\": \"insufficient_quota\"\n    }\n}\n"}
        ```
        ```
                ---------------------------------------------------------------------------
        ZeroDivisionError                         Traceback (most recent call last)
        Cell In[8], line 26
            23 success_rate = len(results) / total_results
            24 print(f"Success rate: {success_rate:.1%}")
        ---> 26 accuracy = sum(results) / len(results)
            27 n = len(results)
            28 z = norm.ppf(0.975)  # 95% confidence interval

        ZeroDivisionError: division by zero
        ```
    - Terminal shows error: 
        ```
        gateway-1     | 2025-08-12T09:35:02.820186Z ERROR inference{otel.name="function_inference" function_name="solve_math_problem" variant_name="gpt_4o_mini_baseline" inference_id="01989da1-f725-73d0-97f3-2a01ae35c146" episode_id="01989da1-f725-73d0-97f3-2a22777fea44"}: tensorzero_core::error: All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {
        gateway-1     |     "error": {
        gateway-1     |         "message": "You exceeded your current quota, please check your plan and billing details. For more information on this error, read the docs: https://platform.openai.com/docs/guides/error-codes/api-errors.",
        gateway-1     |         "type": "insufficient_quota",
        gateway-1     |         "param": null,
        gateway-1     |         "code": "insufficient_quota"
        gateway-1     |     }
        gateway-1     | }
        ```
-  Add OpenAI API usage credit. Restart Jupyter notebook kernel. Run `docker compose down` and `docker compose up` again.
   - Opening localhost:3000 shows
        ```
        gateway-1     | 2025-08-12T09:57:36.880479Z  INFO gateway: TensorZero Gateway is listening on 0.0.0.0:3000
        gateway-1     | 2025-08-12T09:57:36.880540Z  INFO gateway: ├ API Base Path: /
        gateway-1     | 2025-08-12T09:57:36.880546Z  INFO gateway: ├ Configuration: /app/config/tensorzero.toml
        gateway-1     | 2025-08-12T09:57:36.880550Z  INFO gateway: ├ Observability: enabled (database: tensorzero)
        gateway-1     | 2025-08-12T09:57:36.880553Z  INFO gateway: └ OpenTelemetry: disabled
        gateway-1     | 2025-08-12T09:57:48.651011Z  WARN tensorzero_core::error: Route not found: GET /
        ```
    - Opening localhost:4000 shows TensorZero UI
    - Run all Jupyter notebook cells again.
    - Error in the second cell under "Run example"
        ```
        2025-08-12T09:59:54.418884Z  WARN tensorzero_internal::error: Request failed: HTTP status server error (502 Bad Gateway) for url (http://localhost:3000/inference)
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"Rate limit reached for gpt-4o-mini in organization org-2UNBOwAjq6LkaA8Fl347aXVc on requests per min (RPM): Limit 500, Used 500, Requested 1. Please try again in 120ms. Visit https://platform.openai.com/account/rate-limits to learn more.\",\n        \"type\": \"requests\",\n        \"param\": null,\n        \"code\": \"rate_limit_exceeded\"\n    }\n}\n\ngpt_4o_mini_optimized: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"Rate limit reached for gpt-4o-mini in organization org-2UNBOwAjq6LkaA8Fl347aXVc on requests per min (RPM): Limit 500, Used 500, Requested 1. Please try again in 120ms. Visit https://platform.openai.com/account/rate-limits to learn more.\",\n        \"type\": \"requests\",\n        \"param\": null,\n        \"code\": \"rate_limit_exceeded\"\n    }\n}\n"}
        ```
    - Error in the third cell under "Run example"
        ```
        2025-08-12T09:59:56.443204Z  WARN tensorzero::client_input: Deprecation Warning: passing in an object for `content` is deprecated. Please use an array of content blocks instead.
        Output is truncated. View as a scrollable element or open in a text editor. Adjust cell output settings...
        Running test inferences:   0%|          | 1/200 [00:00<02:35,  1.28it/s]
        2025-08-12T09:59:57.209262Z  WARN tensorzero_internal::error: Request failed: HTTP status server error (502 Bad Gateway) for url (http://localhost:3000/inference)
        Error (<class 'tensorzero.types.TensorZeroError'>): TensorZeroError (status code 502): {"error":"All variants failed with errors: gpt_4o_mini_baseline: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {\n    \"error\": {\n        \"message\": \"Rate limit reached for gpt-4o-mini in organization org-2UNBOwAjq6LkaA8Fl347aXVc on requests per min (RPM): Limit 500, Used 500, Requested 1. Please try again in 120ms. Visit https://platform.openai.com/account/rate-limits to learn more.\",\n        \"type\": \"requests\",\n        \"param\": null,\n        \"code\": \"rate_limit_exceeded\"\n    }\n}\n"}
        ```
        ```
        ---------------------------------------------------------------------------
        ZeroDivisionError                         Traceback (most recent call last)
        Cell In[8], line 26
            23 success_rate = len(results) / total_results
            24 print(f"Success rate: {success_rate:.1%}")
        ---> 26 accuracy = sum(results) / len(results)
            27 n = len(results)
            28 z = norm.ppf(0.975)  # 95% confidence interval

        ZeroDivisionError: division by zero
        ```
    - Error in the terminal:
        ```
        gateway-1     | 2025-08-12T10:00:01.104713Z ERROR inference{otel.name="function_inference" function_name="solve_math_problem" variant_name="gpt_4o_mini_baseline" inference_id="01989db8-f173-7400-9523-a7af92abbba3" episode_id="01989db8-f173-7400-9523-a7b3ee82aa66"}:infer{function_name=solve_math_problem variant_name=gpt_4o_mini_baseline otel.name="variant_inference" stream=false}:infer_model_request{model_name=openai::gpt-4o-mini}:infer{model_name="openai::gpt-4o-mini" otel.name="model_inference" stream=false}: tensorzero_core::error: All model providers failed to infer with errors: openai: Error 429 Too Many Requests from openai client: {
        gateway-1     |     "error": {
        gateway-1     |         "message": "Rate limit reached for gpt-4o-mini in organization org-2UNBOwAjq6LkaA8Fl347aXVc on requests per min (RPM): Limit 500, Used 500, Requested 1. Please try again in 120ms. Visit https://platform.openai.com/account/rate-limits to learn more.",
        gateway-1     |         "type": "requests",
        gateway-1     |         "param": null,
        gateway-1     |         "code": "rate_limit_exceeded"
        gateway-1     |     }
        gateway-1     | }
        gateway-1     | 
        ```
        - Rate limit reached due to requests per minute. Have to see how much RPM is needed for this app.
    - TensorZero UI shows 10 inferences, consistent with 10 requests (9,561 input tokens) visible under Usage in the OpenAI API dashboard by `gpt-4o-mini-2024-07-18`.
-  Unable to increase OpenAI usage limits because
    ```
    Increasing your limits
    Your organization is currently in Usage tier 1. Your limits will automatically be increased once you move to the next usage tier based on the criteria outlined below. Visit our usage tiers documentation to learn more about the limits associated with each tier.
    Current tier
    Usage tier 1
    Once the following criteria are met, you'll automatically move to the next tier:
    At least $50 spent on the API since account creation.
    At least 7 days passed since first successful payment.
    View payment history
    Buy credits
    Next tier
    Usage tier 2
    ```