# Kinesis Advantage 360 - Bluetooth Configuration

## Current Bluetooth Strategy

Your Bluetooth controls are integrated into the **mod layer (Layer 3)**, which is accessed by holding the key in the top-right area of your keyboard.

## How to Access Bluetooth Functions

1. **Access the mod layer**: Hold the `mo 3` key (located in top row, right side after &tog 1)
2. **While holding**, press the corresponding number key for Bluetooth functions

## Bluetooth Key Mappings (Layer 3 - mod)

While holding the layer 3 key:

| Key | Function | Description |
|-----|----------|-------------|
| 1 | `BT_SEL 0` | Select Bluetooth profile 0 |
| 2 | `BT_SEL 1` | Select Bluetooth profile 1 |
| 3 | `BT_SEL 2` | Select Bluetooth profile 2 |
| 4 | `BT_SEL 3` | Select Bluetooth profile 3 |
| 5 | `BT_SEL 4` | Select Bluetooth profile 4 |
| (Middle thumb key) | `BT_CLR` | Clear current Bluetooth profile |

## Bluetooth Profile Management

### Switching Devices
1. Hold Layer 3 key (`mo 3`)
2. Press number 1-5 to select the profile for your device
3. Release both keys

### Pairing New Device
1. Clear a profile slot: Hold Layer 3 + press the clear key (middle thumb position)
2. Select the cleared profile: Hold Layer 3 + press the profile number (1-5)
3. Put your device in pairing mode
4. The keyboard will automatically enter pairing mode when selecting an empty profile

### Common Use Cases

**Switching between computer and phone:**
- Profile 0: Main computer
- Profile 1: Phone
- Profile 2: Tablet/Secondary computer
- Profile 3-4: Additional devices

Simply hold Layer 3 and tap the corresponding number to switch.

## Visual Reference

```
Layer 3 (mod) - Hold top-right key to access:

[1:BT0][2:BT1][3:BT2][4:BT3][5:BT4][ 6 ][    ]          [   ][ ][ ][ ][ ][ ][ ]
[     ][     ][     ][     ][     ][   ][BOOT]          [BOOT][ ][ ][ ][ ][ ][ ]
[     ][     ][     ][     ][     ][   ][    ] [BTClr]  [    ][ ][ ][ ][ ][ ][ ]
```

## Troubleshooting

### Can't connect to device
1. Clear the profile (Layer 3 + BT_CLR)
2. Re-select the profile (Layer 3 + number)
3. Re-pair from your device's Bluetooth settings

### Keyboard not responding via Bluetooth
- Check if you're on the correct profile (try cycling through profiles)
- Ensure Bluetooth is enabled in config: `CONFIG_ZMK_BLE=y` ✓ (already set)

### Want to reset all Bluetooth connections
1. Access bootloader mode (Layer 3 + specific key position)
2. Re-flash firmware
3. All profiles will be cleared

## Configuration Status

Your `adv360pro.conf` file has Bluetooth properly enabled:
- ✅ `CONFIG_ZMK_BLE=y` - Bluetooth enabled
- ✅ `CONFIG_ZMK_USB=y` - USB enabled (can use both)

The keyboard supports both USB and Bluetooth connectivity simultaneously.