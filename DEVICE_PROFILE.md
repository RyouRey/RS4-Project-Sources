# Device Profile — itel RS4 / S666LN

- Document version: 1.0
- Status: Partially populated; device audit required
- Purpose: record evidence about the exact phone/firmware, not merely the marketed model.

## 1. Identification

| Field | Value | Status |
|---|---|---|
| Commercial name | itel RS4 | Provisional; confirm on device |
| Model / identifier | S666LN | User-supplied target; verify via properties |
| Android device property | TBD | Not audited |
| Product property | TBD | Not audited |
| Build fingerprint | TBD | Not audited |
| Android release / API | TBD | Not audited |
| itel OS build/version | TBD | Not audited |
| Firmware region/build number | TBD | Not audited |
| Kernel release (`uname -a`) | TBD | Not audited |
| KernelSU / KernelSU Next variant | TBD | User says KernelSU; exact variant unknown |
| Root manager version | TBD | Not audited |
| Boot image / kernel source match | TBD | Not audited |

## 2. Hardware facts to verify

| Component | Initial information | Verification needed |
|---|---|---|
| SoC | MediaTek Helio G99 Ultimate | Record device properties and trusted model documentation |
| CPU | ARM CPU clusters expected for this SoC family | Record `/proc/cpuinfo`, online CPUs, cpufreq policies |
| GPU | Commonly listed as Mali-G57 MC2 | Confirm driver/version and actual exposed controls |
| Display | Marketed as up to 120 Hz | Record supported modes and actual refresh behavior |
| Battery | Marketed capacity around 5,000 mAh | Treat marketing capacity as background, not a tuning control |
| Thermal sensors | Unknown | Read thermal zone `type` and temperatures; do not write thermal nodes |

## 3. Read-only audit commands

Run in a root-capable terminal. These commands are intended to read information only.

```sh
su -c 'getprop ro.product.manufacturer'
su -c 'getprop ro.product.model'
su -c 'getprop ro.product.device'
su -c 'getprop ro.product.name'
su -c 'getprop ro.build.fingerprint'
su -c 'getprop ro.build.version.release'
su -c 'getprop ro.build.version.sdk'
su -c 'uname -a'
su -c 'cat /proc/cpuinfo'
su -c 'ls -la /sys/devices/system/cpu/'
su -c 'ls -la /sys/devices/system/cpu/cpufreq/'
su -c 'for f in /sys/devices/system/cpu/cpufreq/policy*/related_cpus /sys/devices/system/cpu/cpufreq/policy*/scaling_driver /sys/devices/system/cpu/cpufreq/policy*/scaling_governor /sys/devices/system/cpu/cpufreq/policy*/scaling_available_governors /sys/devices/system/cpu/cpufreq/policy*/scaling_available_frequencies; do [ -r "$f" ] && { echo "### $f"; cat "$f"; }; done'
su -c 'for f in /sys/class/thermal/thermal_zone*/type; do [ -r "$f" ] && echo "$f: $(cat "$f")"; done'
su -c 'for f in /sys/class/thermal/thermal_zone*/temp; do [ -r "$f" ] && echo "$f: $(cat "$f")"; done'
su -c 'dumpsys thermalservice'
```

If a command fails or a path does not exist, record that fact; do not try random alternative writes. Some outputs may include personal or device-identifying information; redact serial numbers, account data, and unique identifiers before sharing publicly.

## 4. Capability inventory template

For every candidate interface, record:
- exact path,
- read permission,
- write permission (check permissions only; do not write during audit),
- current value,
- available values/range from a documented companion node,
- which driver or kernel component owns it,
- source/documentation,
- whether the exact firmware has been tested,
- rollback procedure,
- risk level.

## 5. Audit results

No device audit has been supplied yet. All kernel interface availability and behavior remains UNKNOWN.

| Audit item | Result |
|---|---|
| CPUFreq policies | Pending |
| Available governors | Pending |
| Current governor per policy | Pending |
| CPU frequency ranges | Pending |
| GPU driver / interfaces | Pending |
| Thermal zone mapping | Pending |
| Foreground app detection format | Pending |
| KernelSU version and module API | Pending |
| Baseline benchmark | Pending |
| Stock thermal behavior | Pending |

## 6. Update policy

Update this file only when evidence is available. Include the command/source, date, firmware fingerprint, and whether the result was independently repeated. Do not copy values from another phone or custom ROM and mark them as verified for this device.
