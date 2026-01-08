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

Copy `example.env` to `~/.config/vmgputop/config.env` and configure:

- `VM_HOST` - SSH connection (e.g. `user@192.168.1.100`)
- `VM_LOGPATH` - HWiNFO CSV path on the VM
- `HW_*` - Exact column names from your HWiNFO CSV (rename duplicates in HWiNFO if needed)

### Interactive Mode

Set `INTERACTIVE_MODE=TRUE` to show power mode in title bar and enable `p` to run `VM_SCRIPT`.

Mode detection: scans `VM_CPUFREQ` for `VM_CPUFREQ_MARKER`, displays `VM_BOOST` if found, else `VM_LIGHT`.

My setup runs a script that toggles Arch host performance profile, VM guest performance profile, and Afterburner profile. Re-running reverses the changes.

## Usage

`q` quit, `p` toggle power mode
