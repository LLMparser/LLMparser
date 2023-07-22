


## Environment and Requirement
```shell
sh env_init.sh
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