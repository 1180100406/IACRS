# Inter-layer Alignment and Contracting Reward Shaping for Hierarchical Reinforcement Learning (IACRS)
This is a PyTorch implementation for our paper: Inter-layer Alignment and Contracting Reward Shaping for Hierarchical Reinforcement Learning.

Our code is based on official implementation of [GCMR](https://github.com/HaoranWang-TJ/GCMR_ACLG_official) (TNNLS 2024).

# new experiment about reward error
The controller reward is defined as $r_i^l = -\parallel f(s_{i+c})-sg_i \parallel _2$, which can represents reward error to a certain extent. Our new experiment not only shows that IACRS got higher controller reward than GCMR, which means lower reward error, but also proves the accuracy of the effects of the adjacency network.
![reward_error](pic/reward_error.svg)

## Installation
```
conda create -n iacrs python=3.7
conda activate iacrs
./install_all.sh
```

Also, to run the MuJoCo experiments, a license is required (see [here](https://www.roboti.us/license.html)).

## Install MuJoCo
### MuJoCo210
1. Download the MuJoCo version 2.1 binaries for
   [Linux](https://mujoco.org/download/mujoco210-linux-x86_64.tar.gz) or
   [OSX](https://mujoco.org/download/mujoco210-macos-x86_64.tar.gz).
2. Extract the downloaded `mujoco210` directory into `~/.mujoco/mujoco210`.
```
mkdir ~/.mujoco
tar -zxvf mujoco210-linux-x86_64.tar.gz -C ~/.mujoco/
```

If you want to specify a nonstandard location for the package,
use the env variable `MUJOCO_PY_MUJOCO_PATH`.
```
vim ~/.bashrc
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/.mujoco/mujoco210/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/nvidia
source ~/.bashrc
```

### MuJoCo200
1. Download the MuJoCo version 2.0 binaries for
   [Linux](https://www.roboti.us/download/mujoco200_linux.zip) or
   [OSX](https://www.roboti.us/download/mujoco200_macos.zip).
2. Extract the downloaded `mujoco200` directory into `~/.mujoco/mujoco200`.

```
vim ~/.bashrc
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/.mujoco/mujoco200/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/nvidia
source ~/.bashrc
```

***Key license***

Also, to run the MuJoCo experiments using MuJoCo200, a license is required (see [here](https://www.roboti.us/license.html)).
```bash
e.g., cp mjkey.txt ~/.mujoco/mjkey.txt
```

## Usage
### Training & Evaluation

- Ant Maze (U-shape)
```
./scripts/iacrs_ant_maze_u.sh ${reward_shaping} ${timesteps} ${gpu} ${seed}
./scripts/iacrs_ant_maze_u.sh sparse 5e5 0 2
./scripts/iacrs_ant_maze_u.sh dense 5e5 0 2
```

- FetchPickAndPlace
```
./scripts/iacrs_openai_fetch.sh ${env} ${timesteps} ${gpu} ${seed}
./scripts/iacrs_openai_fetch.sh FetchPickAndPlace-v1 5e5 0 2
```

- FetchReach
```
./scripts/iacrs_openai_fetch.sh ${env} ${timesteps} ${gpu} ${seed}
./scripts/iacrs_openai_fetch.sh FetchReach-v1 3e5 0 2
```

- Ant Maze Complex
```
./scripts/iacrs_ant_maze_complex.sh ${reward_shaping} ${timesteps} ${gpu} ${seed}
./scripts/iacrs_ant_maze_complex.sh sparse 10e5 0 2
./scripts/iacrs_ant_maze_complex.sh dense 10e5 0 2
```
