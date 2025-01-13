# Raspberry Pi 4 Model B with CAN Bus Support (64-bit)

This is a modified version of the base Nerves System configuration for the Raspberry Pi 4 Model B, specifically adapted to work with CANable Pro and other USB CAN interfaces. This fork adds native support for CAN bus communication through USB.

## Changes from Original System

This fork includes the following modifications to enable CAN bus support:

1. **Kernel Configuration** (`linux-6.6.defconfig`):
   - Added CAN bus support modules
   - Enabled USB CAN device support
   - Added CANtact/CANable support via CONFIG_CAN_GS_USB
   - Added CAN protocol support (RAW, BCM, Gateway)
   - Enabled SLCAN protocol support
   - Modified USB ACM from modular to built-in

2. **Buildroot Configuration** (`nerves_defconfig`):
   - Added can-utils package for basic CAN utilities
   - Included libsocketcan for SocketCAN user-space support
   - Added socketcand daemon
   - Enabled iproute2 for network configuration
   - Added USB ACM support

3. **Package Renaming** (`mix.exs`):
   - Renamed to `nerves_system_rpi4_can`
   - Updated GitHub organization references to Blue Whale Energy

## Hardware Compatibility

This system has been tested with:
- MKS CANable Pro (USB)
- Other USB-based CAN adapters may work but are untested

| Feature              | Description                      |
| -------------------- | -------------------------------- |
| CPU                  | 1.5 GHz quad-core Cortex-A72 (64-bit mode) |
| Memory               | 1 GB, 2 GB, 4 GB DRAM            |
| Storage              | MicroSD                          |
| Linux kernel         | 6.1 w/ Raspberry Pi patches      |
| CAN Bus             | Yes - via USB (CANable Pro)      |
| USB                 | Yes - enabled by default         |
| GPIO                | Yes - [Elixir Circuits](https://github.com/elixir-circuits) |

## Using

1. Add this package to your dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:nerves_system_rpi4_can, git: "git@github.com:Blue-Whale-Energy/nerves_system_rpi4_can.git", tag: "v1.0.0", runtime: false, targets: :rpi4, nerves: [compile: true]} # edit the tag number
  ]
end
```

2. Set `MIX_TARGET=rpi4` in your environment when building.

## CAN Bus Setup

The system is pre-configured for USB CAN communication and includes several tools for working with CAN interfaces:

### Included Tools
- `can-utils` for sending and receiving CAN frames
- `libsocketcan` for SocketCAN programming
- `socketcand` daemon for remote access to CAN interfaces
- `iproute2` for CAN interface configuration

### Basic Usage
When you plug in the CANable Pro, it should be automatically detected and can be used with the standard Linux SocketCAN interface.

## Original Features

This system maintains all original features of the base `nerves_system_rpi4`, including:
- WiFi support (onboard)
- Camera support (via libcamera)
- Audio support (HDMI/Stereo)
- GPIO, I2C, and standard Raspberry Pi 4 features

For more details on the base system features, please refer to the [original nerves_system_rpi4 repository](https://github.com/nerves-project/nerves_system_rpi4).

## Contributing

If you have any improvements or find any issues, please feel free to:
1. Open an issue at [https://github.com/Blue-Whale-Energy/nerves_system_rpi4_can/issues](https://github.com/Blue-Whale-Energy/nerves_system_rpi4_can/issues)
2. Submit a pull request to [https://github.com/Blue-Whale-Energy/nerves_system_rpi4_can](https://github.com/Blue-Whale-Energy/nerves_system_rpi4_can)

## License

Same as the original nerves_system_rpi4. See LICENSE file for details.