---
name: handle-sparkfun-icm20948-library
description: Index and guide for working with the SparkFun ICM-20948 (ICM_20948) Arduino library. Use to pick the right example sketch and reference docs (DMP, datasheet notes) when integrating the sensor over I2C/SPI.
---

# SparkFun ICM-20948 Arduino Library Helper

This skill is primarily an **index / entry point** into the files in this folder. Use it to quickly choose the right **example sketch** and **reference document** when working with the **SparkFun ICM-20948 Arduino library** (`ICM_20948.h`) and the **SparkFun 9DoF IMU Breakout (ICM-20948)**.

## What’s in this folder (you should consult these)

- **`examples/`**: Arduino `.ino` sketches (best starting point)
- **`DMP.md`**: DMP notes (quaternions, Euler, raw accel, multi-sensor, caveats)
- **`icm20948_datasheet.md`**: datasheet notes / deep reference material

## Example sketches (choose the closest one first)

Start with the simplest example that matches your hardware + goal, then modify incrementally.

- **`examples/Example1_Basics.ino`**
  - **Use for**: first bring-up, basic I2C/SPI wiring, streaming AGMT data.
  - **Key patterns**: `ICM_20948_I2C` / `ICM_20948_SPI`, `begin(...)`, `statusString()`, `dataReady()` → `getAGMT()`.

- **`examples/Example2_Advanced.ino`**
  - **Use for**: beyond basics; more configuration and “how the library is structured”.

- **`examples/Example3_Interrupts.ino`**
  - **Use for**: “data ready” interrupts.
  - **Hardware note**: requires wiring breakout **INT** → MCU pin (`INT_PIN`).

- **`examples/Example4_WakeOnMotion.ino`**
  - **Use for**: low-power / motion-trigger workflows.

- **`examples/Example5_DualSPITest.ino`**
  - **Use for**: SPI-focused setup and/or validating SPI behavior (and conflicts).

### DMP examples (read `DMP.md` too)

Many DMP sketches require enabling DMP support in the SparkFun library:
you may need to edit the library source and enable `ICM_20948_USE_DMP` (see the comments at the top of the DMP examples).

- **`examples/Example6_DMP_Quat9_Orientation.ino`**
  - **Use for**: DMP quaternion orientation (Quat9).
  - **Notes**: includes important DMP enablement instructions in comments.

- **`examples/Example7_DMP_Quat6_EulerAngles.ino`**
  - **Use for**: DMP quaternion (Quat6) and converting to Euler angles.

- **`examples/Example8_DMP_RawAccel.ino`**
  - **Use for**: DMP raw accelerometer output.

- **`examples/Example9_DMP_MultipleSensors.ino`**
  - **Use for**: DMP with multiple sensor outputs enabled at once.

- **`examples/Example10_DMP_FastMultipleSensors.ino`**
  - **Use for**: higher-rate DMP output / performance-focused configuration.

- **`examples/Example11_DMP_Bias_Save_Restore_ESP32.ino`**
  - **Use for**: ESP32-specific flow to save/restore DMP bias.

## When to use this skill

Use this skill when the user:

- Mentions **ICM-20948**, **SparkFun 9DoF IMU Breakout**, or `ICM_20948.h`
- Is writing an Arduino sketch that uses `ICM_20948_I2C` or `ICM_20948_SPI`
- Has initialization issues and sees non-OK `myICM.status`
- Wants “raw vs scaled” explanations and correct units / scaling
- Needs help porting SparkFun examples to a different MCU or interface
- Is working with the **DMP** and needs help interpreting outputs

## How the agent should use this folder

When answering, prefer to:

- **Point to the most relevant example** and explain the minimal edits needed (pins, interface, address, serial port).
- **Cite `DMP.md`** for DMP configuration and interpretation questions.
- **Cite `icm20948_datasheet.md`** only when register-level detail or edge-case behavior is needed.

## Troubleshooting checklist (fast path)

If bring-up fails, ask for/verify:

- Interface: I2C vs SPI
- Board + pin mapping (SDA/SCL or SCK/MISO/MOSI/CS)
- ADR/AD0 jumper setting (I2C address bit)
- Serial output of `myICM.statusString()`
- Whether `dataReady()` ever becomes true

## Minimal code pointers (where to look)

Instead of pasting long code blocks, refer users to:

- `Example1_Basics.ino` for `begin(...)`, `statusString()`, and `dataReady()` → `getAGMT()`
- `Example3_Interrupts.ino` for wiring and `attachInterrupt(...)` with the breakout INT pin
- `Example6..11` for DMP enablement notes and output formats

## Example prompts that should trigger this skill

- “Write an ESP32 sketch to read accel/gyro/mag from SparkFun ICM-20948 over I2C.”
- “My `myICM.begin(Wire, 1)` returns an error—help me debug wiring and address.”
- “Port SparkFun Example1_Basics to SPI with CS on pin 5.”
- “How do I use the DMP quaternion output and convert it to Euler angles?”
- “My magnetometer readings look wrong—what should I verify?”