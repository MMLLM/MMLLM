# Our Vision-Language Pretraining Model

 We released the demo and codes of our large-scale vision-language pre-training models.




## Install

```shell
conda create -n mmllm python=3.10
conda activate mmllm
pip install -r requirements.txt
```





## Demo

### Gradio Web Demo

To launch a Gradio web demo, use the following command. Please note that the model evaluates in the torch.float16 format, which requires a GPU with at least 16GB of memory.

```shell
python mllm/demo/webdemo.py 
```

It is also possible to use it in 8-bit quantization, albeit at the expense of sacrificing some performance.

```shell
python mllm/demo/webdemo.py --load_in_8bit
```

### Server-Client Demo

launch a shikra server:

```shell
python mllm/demo/server.py --model_path /path/to/ckpt
```

a client example is in `mllm/demo/client.py`, check the example results by

```shell
python mllm/demo/client.py
```


## Train

After preparing data in ```docs/data.md```, we use the [acclerate](https://github.com/huggingface/accelerate) package to train the model.
You can train the model using the command:

```shell
accelerate launch --num_processes 4 \
        --main_process_port 23786 \
        mllm/pipeline/pretrain_model.py \
        config/pretrain.py \
  
```


## Inference

After preparing data in ```docs/data.md```, we can use the model to evaluate on the downstream tasks.
You can inference the model using the command:

```shell
accelerate launch --num_processes 4 \
        --main_process_port 23786 \
        mllm/pipeline/pretrain_model.py \
        config/eval_multi.py \
```





## Acknowledgement

This repo benefits from [LLaVA](https://github.com/haotian-liu/LLaVA), [Vicuna](https://github.com/lm-sys/FastChat), [ChatGLM-Efficient-Tuning](https://github.com/hiyouga/ChatGLM-Efficient-Tuning) and [GLIGEN](https://github.com/gligen/GLIGEN).
