# Stochastic Latent Actor-Critic
[[Project Page]](https://alexlee-gk.github.io/slac/) [[Paper]](https://arxiv.org/abs/1907.00953)

**Stochastic Latent Actor-Critic: Deep Reinforcement Learning with a Latent Variable Model,**  
[Alex X. Lee](https://alexlee-gk.github.io/), [Anusha Nagabandi](https://people.eecs.berkeley.edu/~nagaban2/), [Pieter Abbeel](https://people.eecs.berkeley.edu/~pabbeel/), [Sergey Levine](https://people.eecs.berkeley.edu/~svlevine/).  
In *Neural Information Processing Systems (NeurIPS)*, 2020.

## Getting started ###
### Prerequisites
- Linux or macOS
- Python >=3.5
- CPU or NVIDIA GPU + CUDA CuDNN

### Installation
- Clone this repo:
```bash
git clone -b master --single-branch https://github.com/alexlee-gk/slac.git
cd slac
```
- To use the DeepMind Control Suite, follow the instructions in the [`dm_control`](https://github.com/deepmind/dm_control) package.
- To use OpenAI Gym , follow the instructions in the [`gym`](https://github.com/openai/gym) and [`mujoco_py`](https://github.com/openai/mujoco-py) packages.
- Modify the `requirements.txt` file if necessary:
  - Replace `tf-nightly-gpu` with `tf-nightly` if using CPU.
  - Omit `gym`, `mujoco-py`, or `dm_control` accordingly if only using one of the suites.
- Install python packages:
```bash
pip install -r requirements.txt
```
- Install the `tf_agents` package:
```bash
pip install git+git://github.com/tensorflow/agents.git
```
- Install ffmpeg (optional, used to generate GIFs for visualization in TensorBoard).
- For some python installations, the root directory should be added to the `PYTHONPATH`:
```bash
export PYTHONPATH=path/to/slac:$PYTHONPATH
```

### Examples usage
```bash
CUDA_VISIBLE_DEVICES=0 python slac/agents/slac/examples/v1/train_eval.py \
  --root_dir logs \
  --experiment_name slac \
  --gin_file slac/agents/slac/configs/slac.gin \
  --gin_file slac/agents/slac/configs/dm_control_cheetah_run.gin
```
To view training and evaluation information (e.g. learning curves, GIFs of rollouts and predictions), run `tensorboard --logdir logs` and open http://localhost:6006. 

The gin-configurable parameters can be modified using the `--gin_param` flag, e.g. 
```bash
CUDA_VISIBLE_DEVICES=0 python slac/agents/slac/examples/v1/train_eval.py \
  --root_dir logs \
  --experiment_name slac \
  --gin_file slac/agents/slac/configs/slac.gin \
  --gin_file slac/agents/slac/configs/dm_control_cheetah_run.gin \
  --gin_param train_eval.gpu_allow_growth=True \
  --gin_param train_eval.sequence_length=8 \
  --gin_param train_eval.action_repeat=2
```

## Troubleshooting
### `No matching distribution found for tf-nightly-gpu==1.15.0.dev20190821` (or similar) when installing packages in `requirements.txt`.
Upgrade pip: `pip install --upgrade pip`.

### `pkg_resources.VersionConflict: (setuptools 40.8.0 (.../lib/python3.7/site-packages), Requirement.parse('setuptools>=41.0.0'))` when running `tensorboard`.
Upgrade setuptools: `pip install --upgrade setuptools`.

### Other errors
Make sure to exactly use the versions of the python packages in the `requirements.txt` file and in the installation instructions, e.g.
```
pip install --upgrade -r requirements.txt
pip install --upgrade git+git://github.com/tensorflow/agents.git
```

## Citation
If you find this useful for your research, please use the following.

```
@inproceedings{lee2020slac,
  title={Stochastic Latent Actor-Critic: Deep Reinforcement Learning with a Latent Variable Model},
  author={Alex X. Lee and Anusha Nagabandi and Pieter Abbeel and Sergey Levine},
  booktitle={Neural Information Processing Systems (NeurIPS)},
  year={2020}
}
```
