# vmgputop

A terminal-based GPU monitor for NVIDIA GPUs running in a Windows VM, accessed via SSH.

Displays real-time stats from HWiNFO sensor logging in a compact TUI.

```
 ┌── NVIDIA GeForce RTX 4060 ────────────────────┐
 │                                               │
 │ Temp        35°C ░░░░░░░░░░░░░░░░░░░░░░  83°C │
 │ Fan     1500 RPM ██████░░░░░░░░░░░░░░░░   30% │
 │ GPU      210 MHz ░░░░░░░░░░░░░░░░░░░░░░    0% │
 │ Mem     0.4/8.0G █░░░░░░░░░░░░░░░░░░░░░    5% │
 │ MemClk   405 MHz █░░░░░░░░░░░░░░░░░░░░░    5% │
 │ Power    50/115W █████████░░░░░░░░░░░░░   43% │
 │ Volt     0.880 V ██████████████░░░░░░░░   67% │
 │                                               │
 └───────────────────────────────────────────────┘
```

## Requirements

- SSH access to a Windows VM with:
  - NVIDIA GPU with `nvidia-smi`
  - HWiNFO running with sensor logging to CSV
  - PowerShell

## Setup

### 1. Environment Variables

Add SSH host, log path, and colours to your env:

```bash
export VMGPUTOP_HOST="user@192.168.1.100"
export VMGPUTOP_LOGPATH="C:\path\to\log.CSV"
export VMGPUTOP_SCRIPT="/path/to/script"  # Optional: for INTERACTIVE_MODE
export FG="#fcfcfa"
export AQUA="#88c0d0"
export GREEN="#a3be8c"
export YELLOW="#ebcb8b"
export RED="#ff6188"
export ORANGE="#d08770"
export BG4="#5e6987"
```

### 2. HWiNFO Configuration

Configure HWiNFO to log the following sensors to CSV:

- GPU Temperature, GPU Thermal Limit, GPU Core Voltage, GPU Fan1 [RPM],
- GPU Power (Total), GPU Clock, GPU Memory Clock, GPU Fan1 [%],
- GPU Memory Available, GPU Memory Allocated, GPU Core Load

Note: HWiNFO seems to swap the order of the CSV from time to time

### 3. Script Configuration

Edit the script to adjust:

- `INTERACTIVE_MODE` - Enable power mode display in title and P key toggle (TRUE/FALSE)
  - When enabled, requires `VMGPUTOP_SCRIPT` environment variable
- `REFRESH_RATE` - Update interval in seconds
- `VOLTAGE_MIN/MAX` - Voltage range for percentage calculation
- `TEMP_MIN` - Minimum temperature for percentage calculation
- `MEM_CLOCK_MULTIPLIER` - Memory clock multiplier (4 for GDDR6)
- `MEM_CLOCK_BOOST` - Manual memory overclock offset in MHz
