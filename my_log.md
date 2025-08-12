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
