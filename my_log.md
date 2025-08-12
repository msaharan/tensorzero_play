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

