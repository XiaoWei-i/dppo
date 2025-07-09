### Fine-tuning pre-trained policy

All the configs can be found under `cfg/<env>/finetune/`. A new WandB project may be created based on `wandb.project` in the config file; set `wandb=null` in the command line to test without WandB logging.
<!-- Running them will download the default pre-trained policy. -->
<!-- Running the script will download the default pre-trained policy checkpoint specified in the config (`base_policy_path`) automatically, as well as the normalization statistics, to `DPPO_LOG_DIR`.  -->
```console
# Gym - hopper/walker2d/halfcheetah
python script/run.py --config-name=ft_ppo_diffusion_mlp \
    --config-dir=cfg/gym/finetune/hopper-v2
# Robomimic - lift/can/square/transport
python script/run.py --config-name=ft_ppo_diffusion_mlp \
    --config-dir=cfg/robomimic/finetune/can
# D3IL - avoid_m1/m2/m3
python script/run.py --config-name=ft_ppo_diffusion_mlp \
    --config-dir=cfg/d3il/finetune/avoid_m1
# Furniture-Bench - one_leg/lamp/round_table_low/med
python script/run.py --config-name=ft_ppo_diffusion_mlp \
    --config-dir=cfg/furniture/finetune/one_leg_low
```

**Note:** You will most likely encounter the error ```ImportError: libpython3.8.so.1.0: cannot open shared object file: No such file or directory``` when you run fine-tuning. You may fix it by (add to .bashrc if you want it permanently):
```console 
conda env list # print your conda_path
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/joshua/miniforge3/envs/dppo-env/lib
```

### Setting up proxy for downloading models
export http_proxy="http://127.0.0.1:7890"
export https_proxy="http://127.0.0.1:7891"