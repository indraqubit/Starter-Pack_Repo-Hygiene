# PARAMS.md (Template Universal)

## 🎛 Parameter Registry

> **Rule penting:** Semua komentar ID param ditulis di sini, jangan pernah ditaruh di label slider.

---

## Struktur Tabel
| ID              | Label (UI)      | Type    | Range             | Default | Unit | Notes |
|-----------------|-----------------|---------|-------------------|---------|------|-------|
| `domain.param`  | Example Label   | Float   | -24 … +24         | 0       | dB   | Catatan detail |

---

## Example Domains

### 1. IO & Routing
| ID                | Label         | Type  | Range           | Default | Unit | Notes |
|-------------------|---------------|-------|-----------------|---------|------|-------|
| `io.inTrimDb`     | Input Trim    | Float | -24 … +24       | 0       | dB   | Linear gain |
| `io.outTrimDb`    | Output Trim   | Float | -24 … +24       | 0       | dB   | Post gain |
| `io.bypass`       | Bypass        | Bool  | {Off, On}       | Off     | -    | Unity path |

### 2. Dynamics
| ID                  | Label          | Type  | Range         | Default | Unit | Notes |
|---------------------|----------------|-------|---------------|---------|------|-------|
| `dyn.thresholdDb`   | Threshold      | Float | -60 … 0       | -24     | dB   | |
| `dyn.ratio`         | Ratio          | Float | 1 … 20        | 4       | :1   | |
| `dyn.attackMs`      | Attack         | Float | 0.1 … 100     | 10      | ms   | |
| `dyn.releaseMs`     | Release        | Float | 10 … 2000     | 100     | ms   | |

### 3. Meter
| ID                  | Label        | Type   | Range        | Default | Unit | Notes |
|---------------------|--------------|--------|--------------|---------|------|-------|
| `mtr.enable`        | Meter Enable | Bool   | {Off, On}    | On      | -    | Read-only |
| `mtr.momentary`     | Momentary    | Output | -120 … 0     | -120    | dBFS | Window X ms |
| `mtr.shortTerm`     | Short-term   | Output | -120 … 0     | -120    | dBFS | Window Y s |
| `mtr.integrated`    | Integrated   | Output | -120 … 0     | -120    | dBFS | |

---

## Notes
- Semua param numeric SR-agnostic.  
- Semua meter read-only, tidak boleh memodifikasi audio path.  
- Semua range harus dicek (clamp) di code.  
