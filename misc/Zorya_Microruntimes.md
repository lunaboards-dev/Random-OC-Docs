# Zorya μRT
A Zorya Microruntime (μRT) is a runtime enviroment where all the modules are loaded. For most applications, this would be in the EEPROM. But sometimes, a μRT takes the form of a file booted off of the network or over the internet.

## Zorya μRTs

### zyloader
| Field | Value |
| -- | -- |
| Name | zyloader |
| Version | 2.0 |
| Medium | EEPROM |
| Configuration Medium | EEPROM |
| Module Medium(s) | Managed disk, unmanaged disk |
| Requirements | |
| Notes | Normal loader, nothing to see here |

### advloader
| Field | Value |
| -- | -- |
| Name | advloader |
| Version | 1.0 |
| Medium | EEPROM |
| Configuration Medium | EEPROM |
| Module Medium(s) | Managed disk, unmanaged disk |
| Requirements | Tier 1 Data Card |
| Notes | Supports compressed modules and<br>CRC32 hashed BIOS configuration |

### hardloader
| Field | Value |
| -- | -- |
| Name | hardloader |
| Version | 1.0 |
| Medium | EEPROM |
| Configuration Medium | EEPROM |
| Module Medium(s) | Managed disk, unmanaged disk |
| Requirements | Tier 3 Data Card |
| Notes | Hardened loader, enforces signing.<br>Also supports compressed modules. |

### lanloader
| Field | Value |
| -- | -- |
| Name | lanloader |
| Version | 1.0 |
| Medium | Network |
| Configuration Medium | Network |
| Module Medium(s) | Managed disk, unmanaged disk, Network |
| Requirements | Network card |
| Notes | Booted over zlan/ocnet |

### zlmtloader
| Field | Value |
| -- | -- |
| Name | zlmtloader |
| Version | 1.0 |
| Medium | Network |
| Configuration Medium | Network |
| Module Medium(s) | Managed disk, unmanaged disk, network |
| Requirements | Network card |
| Notes | Booted over zlan/minitel |

