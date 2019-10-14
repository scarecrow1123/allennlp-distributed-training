# allennlp-distributed-training

This repo holds code/config for running example AllenNLP experiments with `DistributedDataParallel` support.
The `training_config` directory has two versions of the same set of experiments. The ones in `distributed_data_parallel` 
directory mostly differs with the dataset readers. The dataset readers are replicas of the original ones in AllenNLP, 
with a minor modification to support distributed sampling.

To run the distributed experiments install AllenNLP from [this fork @ https://github.com/scarecrow1123/allennlp/tree/torch-distributed](https://github.com/scarecrow1123/allennlp/tree/torch-distributed).

```bash
conda create -n allennlp_distributed python=3.7
git clone https://github.com/scarecrow1123/allennlp
cd allennlp
git checkout -b torch-distributed
pip install .
```  

`allennlp train training_config/distributed_data_parallel/esim.jsonnet --include-package distributed-training -s output/`

To run without distributed setup, do the usual AllenNLP installation and use experiments in `training_config/ data_parallel/`

#### Comparison