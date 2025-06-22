# Peripheral Side Troubleshooting Guide

## Current Configuration

- **Left Side**: Central (main keyboard, connects to computer)
- **Right Side**: Peripheral (connects to left side via Bluetooth)

## Step-by-Step Fix

### 1. Rebuild and Flash Both Sides

```bash
# Build both sides with the updated configuration
west build -d build/left -b nice_nano -- -DSHIELD=dactyl_manuform_left
west build -d build/right -b nice_nano -- -DSHIELD=dactyl_manuform_right

# Flash both sides
west flash -d build/left
west flash -d build/right
```

### 2. Pairing Process

1. **Flash the left side first** (central)
2. **Flash the right side second** (peripheral)
3. **Wait 30 seconds** after flashing each side
4. **Reset both sides** by pressing the reset button or using the reset key combo

### 3. Connection Process

1. **Left side** should connect to your computer automatically
2. **Right side** should automatically connect to the left side
3. If not, try the **reset key combo** on both sides:
   - Hold `ESC` + `SPACE` + `B` for 3 seconds

### 4. Verify Connection

- Both sides should have **solid LED indicators** (not blinking)
- Try typing on both sides - both should work
- Check your computer's Bluetooth settings for the keyboard

### 5. If Still Not Working

1. **Clear Bluetooth bonds** on both sides:
   - Hold `ESC` + `SPACE` + `BACKSPACE` for 3 seconds
2. **Reset both sides** and try pairing again
3. **Check battery levels** on both sides
4. **Ensure both sides are within 1-2 feet** of each other

### 6. Debug Mode (Optional)

If still having issues, uncomment these lines in `config/dactyl_manuform.conf`:

```
CONFIG_ZMK_USB_LOGGING=y
CONFIG_ZMK_BLE_LOGGING=y
```

Then rebuild and check the logs via USB connection.

## Common Issues

- **Peripheral side not connecting**: Usually a pairing issue, try clearing bonds
- **Intermittent connection**: Check battery levels and distance between sides
- **One side not responding**: May need to reflash that specific side
