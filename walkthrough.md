Go to [exosphere](https://jetstream2.exosphere.app/exosphere/)

Click "Add allocation"

![add allocation](images/add_allocation.png)

Click Add ACCESS Account

![add account](images/add_account.png)

Select ACCESS CI (XSEDE) under "Select an Identity Provider" and click "LOG ON". Enter your ACCESS ID and Password and complete 2FA login

![login](images/login_to_access.png)

Select "CIS240457 — AI Agents on Jetstream2 Training for UH" and click "Choose"

![select allocation](images/select_allocation.png)

Click the allocation tile that was added

![allocations](images/allocations.png)

Click "Create" in the top right corner and click "Instance" in the dropdown

![create instance](images/create_instance.png)

Select Ubuntu 24.04

![ubuntu](images/ubuntu.png)

Name your instance llm-tutorial-<your_last_name> or something similar. This name must be unique so make sure to include your last name or another unique identifier. Select "g3.small" as the flavor and click "Create"

![instance config](images/instance_config.png)

Click on the "Instances" tile and select the VM you just created. It may take a few minutes for the instance to initialize and be ready to use.

![instance](images/instance.png)

Open a terminal and ssh to your VM. You can find the IP address under Credentials in your instance details. Your username will be exouser. Once your instance is fully instantiated there should be a "Show" button next to the Passphrase. This will be your password.

![credentials](images/credentials.png)

Next you will set up an LLM on your instance using the tutorial [here](https://docs.jetstream-cloud.org/general/llm/)

If you have not requested access to the meta-llama models on hugging face you can replace this with [TinyLlama/TinyLlama-1.1B-Chat-v1.0](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0). This model is a bit more memory intensive than the meta models, so you will need to add some additional parameters to get this to work with the small instance you created. In this case replace "vllm serve "meta-llama/Llama-3.2-1B-Instruct" --max-model-len=8192" in the tutorial with "vllm serve "TinyLlama/TinyLlama-1.1B-Chat-v1.0" --max-model-len 2048 --gpu_memory_utilization 0.85 --enforce-eager". Make sure to also replace the command in /etc/systemd/system/vllm.service under the "ExecStart" definition.