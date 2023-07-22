## Structure
We present LLMparser repository structure below.

```
.
├── LLMs
│   ├── chatglm.sh
│   ├── flan-t5-base.sh
│   ├── flan-t5-small.sh
│   └── llama.sh
├── README.md
├── chatglm
│   ├── eval.py
│   ├── modeling_chatglm.py
│   ├── run_copy.sh
│   └── train.py
├── data_sampling.py
├── docs
├── env_init.sh
├── evaluate
│   └── evaluator.py
├── fine_tuned_model
├── flan-t5
│   └── train.py
├── llama
│   ├── 1.py
│   ├── Dockerfile
│   ├── cross_eval.py
│   ├── docker-compose.yml
│   ├── eval.py
│   ├── export.sh
│   ├── export_hf_checkpoint.py
│   ├── finetune.py
│   ├── pyproject.toml
│   ├── run.sh
│   └── utils
│       ├── README.md
│       ├── __init__.py
│       ├── __pycache__
│       │   ├── __init__.cpython-39.pyc
│       │   └── prompter.cpython-39.pyc
│       ├── callbacks.py
│       └── prompter.py
├── logs
│   └── ...
├── output
└── requirements.txt
```


## Environment 
### Requirement
```shell
sh env_init.sh
```

### Large Language Models

To download the Large Language Models:
```shell
cd LLMs
sh flan-t5-base.sh
```


## Data sampling

Sample 50 logs from Mac dataset
```shell
python train.py --project "Mac" \
                --shot 50
```


## Fine-tune and Inference

Flan-T5-base or Flan-T5-small (fine-tuned with 50 shot)
```shell
cd flan-t5
python train.py --model "flan-t5-base"\
                --num_epochs 30 \
                --learning_rate 5e-4 \
                --train_percentage "cross" \
                --validation "validation" \
                --systems "Mac,Android,Thunderbird,HealthApp,OpenStack,OpenSSH,Proxifier,HPC,Zookeeper,Hadoop,Linux,HDFS,BGL,Windows,Apache,Spark"
```

LLaMA (fine-tuned with 50 shot)
```shell
cd llama
sh run.sh 0.025
```

ChatGLM (fine-tuned with 50 shot)
```shell
cd chatglm
sh run.sh 0.025
```

## Evaluation

Evaluate LLM parsing result on certain training dataset size (Flan-T5-base result on 50 shots)
```shell
cd evaluate
python evaluator.py --model "flan-t5-base" \
    --train_percentage "0.025" \
    --systems "Mac,Android,Thunderbird,HealthApp,OpenStack,OpenSSH,Proxifier,HPC,Zookeeper,Hadoop,Linux,HDFS,BGL,Windows,Apache,Spark" 
```
