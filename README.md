# FavoritCoinMiner

High-performance GPU miner for Soteria (SOTER) cryptocurrency using X12R algorithm.

## Features

- ⚡ **CUDA-optimized** mining for NVIDIA GPUs
- 🔄 **X12R algorithm** with automatic rotation of 12 hashing functions
- 📊 **Stratum protocol** support for pool mining
- 💎 **Solo mining** capability
- 🎯 **Low memory footprint** and efficient hash computation

## Supported Algorithms

- **soterg** (X12R) - Soteria native algorithm

## Installation

### Download
Download the latest release from GitHub:
```bash
wget https://github.com/FavoritCoin/Soteria/releases/download/v2.0.0/favoritcoinminer_linux.zip
```

Or using curl:
```bash
curl -L -O https://github.com/FavoritCoin/Soteria/releases/download/v2.0.0/favoritcoinminer_linux.zip
```

### Extract
```bash
# Install unzip if not already installed
sudo apt install unzip

# Extract archive
unzip favoritcoinminer_linux-x64.zip

# Navigate to directory
cd favoritcoinminer

# Make executable
chmod +x favoritcoinminer
```

### Run

**Note:** Connection parameters may vary depending on the pool. Below are examples for different pools.

```bash
# Example 1: Pool with worker name
./favoritcoinminer -a soterg -o stratum+tcp://pool.example.com:3032 -u YOUR_WALLET.worker -p x

# Example 2: Pool with coin parameter
./favoritcoinminer -a soterg -o stratum+tcp://eu.coin-miners.info:25100 -u YOUR_WALLET -p c=SOTER

# Example 3: Solo mining mode
./favoritcoinminer -a soterg -o stratum+tcp://pool.example.com:3032 -u YOUR_WALLET -p c=SOTER,m=solo

# Example 4: Pool with difficulty setting
./favoritcoinminer -a soterg -o stratum+tcp://pool.example.com:3032 -u YOUR_WALLET -p c=SOTER,d=0.1
```

**Always check your pool's documentation for correct connection parameters!**

## Dev Fee

**How it works:**
- Every **60 minutes**, the miner reconnects to the pool with the developer's wallet for **5 minutes**
- Fee collection happens via automatic reconnection (similar to Phoenix/TeamRedMiner approach)
- **No share stealing** - clean disconnect/reconnect mechanism
- All reconnections are logged with timestamps

**Transparency:**
- Dev wallet: `ShJnw2TGPNw6R9VT5t3td73fJdzbYNB891`
- You can verify dev mining periods in the console output

**Example output:**
```
[DevFee] 🔄 Reconnecting to DEV wallet...
[DevFee] ✅ Mining to DEV wallet: ShJnw2TGPN...
... mining for 5 minutes ...
[DevFee] 🔄 Reconnecting to MAIN wallet...
[DevFee] ✅ Mining to MAIN wallet: Safr5Vc9Ue...
```

## Performance

Expected hashrate depends on your GPU:
- RTX 3080: ~45-50 MH/s
- RTX 3070: ~40-45 MH/s
- RTX 2070: ~30-35 MH/s
- GTX 1080 Ti: ~35-40 MH/s
- GTX 1070: ~25-30 MH/s

## Requirements

- NVIDIA GPU with CUDA support
- CUDA Toolkit 10.0 or higher
- Linux (Ubuntu/Debian recommended)

## Command Line Options

```bash
./favoritcoinminer [options]

Main options:
  -a, --algo=ALGO       mining algorithm (soterg)
  -o, --url=URL         pool URL (stratum+tcp://...)
  -u, --user=USERNAME   wallet address
  -p, --pass=PASSWORD   password
  -i, --intensity=N     GPU intensity (8-25, default: auto)
  -t, --threads=N       number of CUDA threads
  -q, --quiet           minimal output
  -D, --debug           debug mode
  -B, --background      run in background
  --no-color            disable colored output
```

## Usage Examples

### Pool mining with custom settings
```bash
./favoritcoinminer -a soterg \
  -o stratum+tcp://eu.coin-miners.info:25100 \
  -u Safr5Vc9UeuH3BzYzwuAjRKJtsinSUFysD \
  -p c=SOTER \
  -i 20
```

### Solo mining
```bash
./favoritcoinminer -a soterg \
  -o stratum+tcp://localhost:3032 \
  -u YOUR_WALLET_ADDRESS \
  -p c=SOTER,m=solo
```

### Quiet mode (for scripts)
```bash
./favoritcoinminer -a soterg -o stratum+tcp://... -u ... -p ... -q
```

## Troubleshooting

### Error: "CUDA error"
- Make sure NVIDIA drivers are installed: `nvidia-smi`
- Try lowering intensity: `-i 18`

### Low hashrate
- Check GPU temperature
- Increase GPU power limit
- Close other GPU applications

### Startup error
- Install dependencies: `sudo apt install build-essential libcurl4-openssl-dev libssl-dev`
- Check CUDA version: `nvcc --version`

## Version

**Current version:** 2.0.0

Major changes in 2.0:
- Added X12R algorithm support (Soteria)
- Implemented transparent dev fee via reconnection
- Performance optimization for CUDA 10.0+
- Improved Stratum connection stability

## License

GPL v3

## Support

For issues and questions, please open an issue on GitHub:
https://github.com/FavoritCoin/Soteria/issues

## Credits

Based on ccminer by tpruvot and GPU miners community.
