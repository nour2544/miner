# Real-Time Miner Setup Guide

This guide covers setting up a miner for real-time serving of Laxaum AI user requests.

## Prerequisites

- Docker
- Python 3.8+
- Hugging Face account and API token
- WANDB token for training

## Setup Steps

1.Clone the repo

```bash
git clone https://github.com/nour2544/miner.git
cd miner
```

2.Install system dependencies:

```bash
sudo -E ./bootstrap.sh
source $HOME/.bashrc
source $HOME/.venv/bin/activate
```

3.Install the python packages:

```bash
task install
```

** FOR DEV **

```bash
pip install -e '.[dev]'
```

4.Set up your wallet:

You prob know how to do this, but just in case:

Make sure you have bittensor installed to the latest version then:

```bash
btcli wallet create --wallet.name miner
```

To check see your wallet address.

```bash
btcli wallet list
```

5.Register to the subnet.

```bash
btcli subnets register --netuid 2 \
--wallet-name miner \
--hotkey miner-hotkey \
--network ws://54.252.195.55:9945
```

6.Register on metagraph

Then register your IP on the metagraph using fiber. Get your external ip with `curl ifconfig.me`.

```bash
fiber-post-ip \
  --netuid 2 \
  --subtensor.chain_endpoint ws://54.252.195.55:9945 \
  --external_port 7999 \
  --wallet.name miner \
  --wallet.hotkey miner-hotkey \
  --external_ip YOUR_PUBLIC_IP
```

7.Configure environment variables:

NOTE: You will need a wandb token & a huggingface token.
Replace the following wandb and huggingface tokens with yours.

```
WALLET_NAME=miner
HOTKEY_NAME=miner-hotkey
SUBTENSOR_NETWORK=local
NETUID=2
ENV=dev
SUBTENSOR_ADDRESS=ws://54.252.195.55:9945
MIN_STAKE_THRESHOLD=1000
REFRESH_NODES=True
IS_VALIDATOR=False
WANDB_TOKEN=
HUGGINGFACE_USERNAME=
HUGGINGFACE_TOKEN=
```

8.Start the miner service:

```bash
task miner
```

## Additional Resources
