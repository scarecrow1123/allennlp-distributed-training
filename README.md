# allennlp-distributed-training

This repo holds code/config for running example AllenNLP experiments with `DistributedDataParallel` support.
The `training_config` directory has two versions of the same set of experiments. The ones in `distributed_data_parallel` 
directory mostly differs with the dataset readers. The dataset readers are replicas of the original ones in AllenNLP, 
with a minor modification to support distributed sampling.

To run the distributed experiments install AllenNLP from [this fork @ https://github.com/scarecrow1123/allennlp/tree/torch-distributed](https://github.com/scarecrow1123/allennlp/tree/torch-distributed).

```bash
conda create -n allennlp_distributed python=3.7
conda activate allennlp_distributed
git clone https://github.com/scarecrow1123/allennlp
cd allennlp
git checkout -b ddp-3 
pip install .
```  

`allennlp train training_config/distributed_data_parallel/esim.jsonnet --include-package distributed-training -s output/`

To run without distributed setup, do the usual AllenNLP installation and use experiments in `training_config/ data_parallel/`

#### Speed Comparison: Time taken to train one epoch (averaged over 3 epochs) 

GPU - 2080 Ti

NOTE: The time reported **does not** correspond to the `training_duration` metric. This is the time taken by the `Trainer._train_epoch` method.

| Experiment | Single GPU | 2x Data Parallel | 2x Distributed | 4x Data Parallel | 4x Distributed |
|------------|------------|------------------|----------------|------------------|----------------|
| esim.jsonnet (400K SNLI samples) | 4m 15s | NA | NA | 4m 30s | 2m 13s |
| bidaf.jsonnet | 5m 44s | NA | NA | 4m 10s | 2m 5s |    
