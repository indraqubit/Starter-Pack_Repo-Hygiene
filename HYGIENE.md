# HYGIENE.md

## 🎛 Minimal Portability Hygiene (Universal)

### 1. Param IDs
- Skema: `domain.paramName` (mis. `io.guardOn`, `lim.ceilingDbtp`).  
- Semua param dicatat di `PARAMS.md`.  
- **Guardrail:** ❌ Jangan pernah taruh komentar di label sliders.  
  - Salah:
    ```js
    slider1:gain=0<-24,24,0.1>Gain // mainGain
    ```  
  - Benar:
    ```js
    slider1:gain=0<-24,24,0.1>Gain
    // Param ID: io.gain
    ```

### 2. Koefisien
- Hitung di `@slider` / saat sample rate ganti.  
- Loop audio hanya apply hasil.

### 3. SR-agnostic
- Simpan `sr = srate`.  
- Kalau `srate` berubah → recalc semua koef SR-dependent sekali saja.

### 4. Single-writer
- Tulis `spl0/spl1` hanya sekali di akhir blok.  
- Antar-blok lewat buffer standar (`nextL/nextR`).

### 5. Bypass
- Definisi konsisten: audio lewat, efek dilewati.  
- Final guard selalu setelah trims.

### 6. Latency
- Tiap blok jelas: `latencySamples = 0` (kecuali ada delay).

### 7. State
- State internal tertutup.  
- Komunikasi antar-blok hanya via buffer + meter vars.

### 8. Naming
- Prefix domain: `io_*`, `mtr_*`, `lim_*`, `la_*`, `xo_*`, `sc_*`, `gn_*`.  
- File/folder rapih: `/DSP/Blocks/*`, `/DSP/Pipeline.*`, `/Params.*`.

### 9. No quirks
- Jangan pakai `e` notasi ilmiah (JSFX).  
- Jangan pakai `^` utk pangkat (JSFX = XOR).  
- Semua var harus di-init dulu sebelum dipakai.

### 10. Versi
- Semver (`x.y.z`).  
- Header: `version: x.y.z` + 1–2 baris changelog mini.

---

## 🛡 Guardrails Anti-Error Dini
1. Clamp slider ke range valid.  
2. NaN/Inf kill: epsilon di log/sqrt.  
3. Denormal kill: flush-to-zero / tambah noise kecil.  
4. Final guard setelah out-trim.  
5. SR tripwire: recalc sekali saat `srate` berubah.  
6. Meter read-only, tidak sentuh audio path.  
7. Bypass test: unity path konsisten.  
8. Assertions ringan: dev mode cek finite/valid.

---

## ✅ Quick QA Sheet (per blok)
- [ ] Unity path Off → null test pass.  
- [ ] Bypass → sesuai definisi, tidak bocor.  
- [ ] Koef stabil, tidak dihitung di loop.  
- [ ] SR switch 44.1/48/96k → perilaku sama.  
- [ ] Single-writer: audit hanya 1 write.  
- [ ] No NaN/Inf/denormal.  
- [ ] Latency report benar.  
- [ ] Clamp/constraint jalan.
