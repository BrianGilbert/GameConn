# GameConn

**You have the conn.**

> [!IMPORTANT]
> **In active development. The source code isn't public yet.** This
> repository describes where GameConn is today. The code stays private
> while I find out whether [sponsorship](https://github.com/sponsors/BrianGilbert)
> can cover the cost of developing it. The aim is to release GameConn
> free of charge.

GameConn connects games to the hardware around you. It receives live
telemetry from any game speaking the
[OGSA Telemetry Standard (OGSA-TS)](https://github.com/Open-Game-Standards-Alliance/OGSA-Telemetry-Standard)
on your local network and drives your devices with it: motion rigs,
haptics and more, each through its own plugin, all from one app.

Any OGSA-TS source works: games with a native
[engine plugin](https://github.com/Open-Game-Standards-Alliance), games
running one of the
[loader mods](https://github.com/Open-Game-Standards-Alliance#loader-mods),
and games whose own telemetry output is translated by
[OGSA-TS Bridge](https://github.com/BrianGilbert/ogsa-ts-bridge).

## Where it is today

### Devices

| Device | What GameConn does with it | State |
| --- | --- | --- |
| **Yaw motion simulators** | Finds rigs on the network, drives yaw, pitch and roll at the rig's native 100 Hz, plus vibration, with the rig's own settings (power, tilt and yaw limits) available in the app. Reads the rig's actual position back, ready for VR motion compensation. | Validated end to end with the Yaw Emulator, playing Hot Wheels Unleashed through the [BepInEx loader mod](https://github.com/BrianGilbert/bepinex-ogsa-ts) |
| **DOF Reality platforms** | Drives SMC3 motor controllers for 3, 4 and 6 degree-of-freedom platforms, including platforms that span several boards. | **Untested.** Written against the SMC3 protocol but not yet run on a real platform |
| **Audio exciters** | Turns telemetry into engine rumble, road texture and wind for bass shakers and other tactile transducers, on any audio output. | Implemented |

### The app

- **Per-game profiles.** Each game gets a profile that maps its telemetry
  onto any number of devices, with ranges, transforms and conditions, and
  overrides per vehicle type when the game reports one.
- **Works out of the box.** Without a profile, motion devices follow the
  game's motion directly, and moving in the right direction is guaranteed
  by tests. An auto-mapping advisor proposes a starting profile from a
  short capture of the game's telemetry.
- **Motion cueing.** Washout and tilt coordination, the techniques motion
  simulators use to make sustained acceleration feel right.
- **Safety first.** Devices only move once they're armed, and can be
  paused at any time. When a game reports that it's paused, motion rigs
  ease gently to their neutral position and haptics go quiet, then ease
  back when the game resumes.
- **Desktop app and headless daemon.** A GUI for setup and live
  monitoring, and a command-line daemon for running unattended.
- **Built for low latency.** Telemetry reaches each device's output loop
  without queues or locks on the way.

GameConn is built cross-platform, targeting at least **Windows and
Linux**. Its core uses no Windows-only APIs and its interface runs on
both; on Linux it runs natively, receiving telemetry from games running
under Steam Proton. Development and testing so far have been on Windows.

## What's next

- Haptic vests and cockpit dash panels, driven by the standard's event
  frames (impacts, gunfire and other stimuli)
- VR motion compensation using the rig position GameConn already reads
- Publishing the device plugin specification, so anyone can add support
  for their hardware. This will be published as soon as possible.
- Loading third-party device plugins
- An end-to-end latency meter
- Linux testing and packaging

## Follow along

- **Discord:** [support and discussion](https://discord.gg/yyCp5D2Ccp)
- **Sponsor:** [GitHub Sponsors](https://github.com/sponsors/BrianGilbert).
  Sponsorship decides how quickly GameConn reaches a public release, and
  whether it can be released for free. It also moves the rest of the work
  forward: the OGSA standards and their SDKs, the loader mods and
  OGSA-TS Bridge.
- **The standard:** [Open Game Standards Alliance](https://github.com/Open-Game-Standards-Alliance)
