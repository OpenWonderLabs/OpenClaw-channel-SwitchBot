# SwitchBot Channel for OpenClaw

> Connect your SwitchBot smart home devices to OpenClaw platform for real-time device status monitoring

## 📖 Project Overview

SwitchBot Channel is an official channel plugin for the OpenClaw platform that receives real-time SwitchBot device status changes via MQTT protocol. Whether it's contact sensors, temperature/humidity meters, or smart plugs, you can monitor device status in real-time through OpenClaw and set up intelligent notifications.

## ✨ Features

- 🔄 **Real-time Sync**: Receive device status via MQTT in real-time
- 🏠 **Device Compatibility**: Support for all mainstream SwitchBot devices
- 🔑 **Auto Authentication**: Intelligent credential management with auto-renewal
- 🚨 **Smart Notifications**: Send notifications only for important events to avoid interruptions
- 🔧 **Zero Configuration**: Out-of-the-box functionality with just SwitchBot Token and Secret
- 📊 **History Records**: Local storage of device status history
- 🛡️ **High Availability**: Auto-reconnection with automatic recovery after network interruptions

## 🚀 Quick Start

### System Requirements

- **OpenClaw**: >= 2026.1.0
- **Node.js**: >= 20.0.0
- **SwitchBot App**: Latest version

### Step 1: Install Plugin

#### Prerequisites

Before installing the plugin, ensure your OpenClaw environment has the required dependencies:

```bash
# Install pnpm if not already installed
npm install -g pnpm

# Install dependencies in your OpenClaw installation
pnpm install
```

#### Installation

```bash
# Install plugin from npm
openclaw plugins install @switchbot/openclaw-channel-switchbot

# Verify installation
openclaw plugins list
```

### Step 2: Get SwitchBot Credentials

1. **Open SwitchBot App**
2. **Enter Developer Options**:
   - Tap "Settings" in bottom right
   - Find and tap "Developer Options"
   - If this option doesn't exist, ensure the App is updated to the latest version

3. **Get Credentials**:
   - Record the **Token** (64-character string)
   - Record the **Secret** (32-character string)

> ⚠️ **Important**: Keep your Token and Secret secure and don't share them with others

### Step 3: Configure OpenClaw

Edit OpenClaw configuration file `~/.openclaw/openclaw.json`:

```json
{
  "plugins": {
    "entries": {
      "openclaw-channel-switchbot": {
        "enabled": true
      }
    }
  },
  "channels": {
    "switchbot": {
      "enabled": true,
      "token": "your_switchbot_token_here",
      "secret": "your_switchbot_secret_here"
    }
  }
}
```

### Step 4: Start Service

```bash
# Restart OpenClaw Gateway
openclaw gateway restart

# Check plugin status
openclaw status
```

## ⚙️ Configuration Details

### Basic Configuration

```json
{
  "channels": {
    "switchbot": {
      "enabled": true,
      "token": "xxxx",
      "secret": "xxxx"
    }
  }
}
```

## 📱 Usage Guide

### Device Status Monitoring

After the plugin starts, it will automatically receive status changes from all devices. You can view them using:

```bash
# View device status
openclaw devices list switchbot

# View specific device
openclaw devices show <device_id>
```

## 🔍 Troubleshooting

### Common Issues

#### Q: Plugin fails to start
**A**: Check configuration

```bash
# Check configuration syntax
openclaw config validate

# View detailed errors
openclaw gateway logs --follow
```

### Debug Mode

Enable detailed logging for troubleshooting:

```json
{
  "logging": {
    "level": "debug",
    "channels": {
      "switchbot": "debug"
    }
  }
}
```

View logs:
```bash
# View real-time logs
tail -f ~/.openclaw/logs/gateway.log | grep "SwitchBot"

# View error logs
openclaw gateway logs --level error
```

### Reset Plugin

If you encounter serious issues, you can reset the plugin:

```bash
# Stop service
openclaw gateway stop

# Clear plugin cache
rm -rf ~/.openclaw/cache/plugins/switchbot

# Restart
openclaw gateway start
```

**Made with ❤️ by the SwitchBot Team**