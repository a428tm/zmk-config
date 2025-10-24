# Kinesis Advantage 360 - Auto-Shift Configuration Summary

## Overview
This document summarizes the auto-shift behavior configuration for your ZMK keymap. Auto-shift eliminates the need for the Shift key by using hold duration to produce shifted characters.

## Auto-Shift Configuration

### Timing Settings
- **Tapping Term**: 300ms (hold duration to trigger shifted character)
- **Quick Tap**: 150ms (window for quick repeated taps)
- **Flavor**: tap-preferred (prioritizes normal typing)

## How Auto-Shift Works

### For Letters (A-Z)
| Action | Result | Example |
|--------|--------|---------|
| Quick tap (<300ms) | Lowercase letter | Tap "j" → j |
| Hold (≥300ms) | Uppercase letter | Hold "j" → J |
| Quick double tap | Two lowercase | Tap "l" twice → ll |

### For Numbers (0-9)
| Key | Tap (<300ms) | Hold (≥300ms) |
|-----|--------------|---------------|
| 1 | 1 | ! |
| 2 | 2 | @ |
| 3 | 3 | # |
| 4 | 4 | $ |
| 5 | 5 | % |
| 6 | 6 | ^ |
| 7 | 7 | & |
| 8 | 8 | * |
| 9 | 9 | ( |
| 0 | 0 | ) |

### For Symbols
| Key | Tap (<300ms) | Hold (≥300ms) |
|-----|--------------|---------------|
| = | = | + |
| - | - | _ |
| [ | [ | { |
| ] | ] | } |
| \ | \ | \| |
| ; | ; | : |
| ' | ' | " |
| , | , | < |
| . | . | > |
| / | / | ? |
| ` | ` | ~ |

## Key Mapping Changes

### All Alphabetic Keys
Every letter key now uses auto-shift:
- `&as LS(A) A` - Tap for 'a', hold for 'A'
- `&as LS(B) B` - Tap for 'b', hold for 'B'
- ... and so on for all letters

### All Numeric Keys
Every number key now produces symbols when held:
- `&as EXCL N1` - Tap for '1', hold for '!'
- `&as AT N2` - Tap for '2', hold for '@'
- ... and so on for all numbers

## Usage Examples

### Typing Regular Text
- "hello" → tap h, e, l, l, o (all quick taps)
- "Hello" → hold h (≥300ms), tap e, l, l, o
- "HELLO" → hold each key for ≥300ms

### Typing Symbols
- Email "user@example.com" → tap user, hold 2 (@), tap example.com
- "Hello!" → hold h, tap ello, hold 1 (!)
- "$100" → hold 4 ($), tap 100

### Typing Code
```
// C++ example
#include <iostream>  // hold 3 for #, hold comma for <, hold dot for >

int main() {         // hold 9 and 0 for ()
    return 0;        // hold ; for :
}
```

## Adjusting the Timing

If you need to fine-tune the auto-shift behavior:

### Too Many Accidental Capitals
**Problem**: Getting capitals when you don't want them
**Solution**: Increase `tapping-term-ms` in the `as` behavior (try 350ms or 400ms)

### Capitals Not Activating
**Problem**: Holding but still getting lowercase
**Solution**: Decrease `tapping-term-ms` (try 250ms)

### Can't Type Repeated Letters
**Problem**: "look" becomes "Look"
**Solution**: Increase `quick-tap-ms` (try 175ms or 200ms)

Edit these values in `config/adv360pro.keymap`:
```c
as: auto_shift {
    compatible = "zmk,behavior-hold-tap";
    label = "AUTO_SHIFT";
    #binding-cells = <2>;
    tapping-term-ms = <300>;  // Adjust this value
    quick-tap-ms = <150>;     // Adjust this value
    flavor = "tap-preferred";
    bindings = <&kp>, <&kp>;
};
```

## Important Notes

1. **Physical Shift Keys**: Still available on your keyboard for compatibility
2. **Caps Lock**: Still works normally for all-caps typing
3. **Layer Switching**: Space and Enter still have layer-tap functionality
4. **Modifiers**: Ctrl, Alt, GUI keys work normally (not auto-shifted)

## Quick Reference

```
Auto-Shift Active on ALL:
- Letters: a-z → A-Z
- Numbers: 0-9 → symbols
- Symbols: ,.;'[]\ → <.:"{}\|

Hold Duration: 300ms
Quick Repeat: 150ms

NO Auto-Shift on:
- Tab, Esc, Backspace, Delete
- Arrow keys
- Modifier keys (Ctrl, Alt, Shift, GUI)
- Function/Layer keys
```

## Reverting to Standard Typing

To disable auto-shift and return to normal keyboard behavior:
1. Replace all `&as X Y` with `&kp Y` in the keymap
2. Example: `&as LS(A) A` → `&kp A`
3. Rebuild and flash firmware

## Building and Flashing

After making changes:
1. Commit and push to your GitHub repository
2. GitHub Actions will automatically build the firmware
3. Download the `.uf2` files from the Actions tab
4. Flash to both keyboard halves