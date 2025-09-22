# Standard Minimal Portability Hygiene (Universal)

[![SemVer](https://img.shields.io/badge/semver-0.1.0-blue)](./CHANGELOG.md)
![Portability](https://img.shields.io/badge/portability-hygiene%20locked-green)
![Guardrails](https://img.shields.io/badge/guardrails-ON-red)

## 📖 Overview

**Standard Minimal Portability Hygiene (SMPH)** adalah rulebook ringan tapi brutal untuk coding DSP (JSFX, JUCE/C++, AAX, dll.).
Tujuannya: bikin pipeline **stabil, portable, scalable** dan **anti-error dini**.

Dokumen ini dipakai sebagai **aturan dasar universal** di semua blok DSP project **Infinites Studio** maupun plugin lain.

---

## 🎛 Prinsip Utama

* 🔒 **Param IDs terkunci** → semua dicatat di [`PARAMS.md`](./PARAMS.md)
* 🚫 **Jangan pernah taruh komentar di label sliders**
* 📉 Koef dihitung sekali (param/SR update), bukan di sample loop
* 🎚 **Single-writer audio path** → output ditulis sekali di akhir
* 🛡 Bypass konsisten → unity path, guard tetap jalan sesuai kontrak
* ⏱ SR-agnostic → recalc saat `srate` berubah
* 📦 State internal tertutup → komunikasi antar blok via buffer standar
* ❌ No quirks: jangan pakai `e` notasi ilmiah, jangan pakai `^` untuk pangkat (XOR di JSFX)
* 📑 Versioning SemVer + catatan perubahan di [`CHANGELOG.md`](./CHANGELOG.md)

---

## 🛡 Guardrails Anti-Error

* Clamp slider ke range valid
* Kill NaN/Inf (pakai epsilon di `log/sqrt`)
* Denormal kill (flush-to-zero / noise kecil)
* Final guard setelah out-trim
* SR tripwire: recalc koef saat `srate` berubah
* Meter read-only (tidak menyentuh audio path)
* Bypass harus unity path
* Assertion ringan di dev mode

---

## ✅ Quick QA per Blok

* [ ] Unity path Off → null test pass
* [ ] Bypass → sesuai definisi
* [ ] Koef stabil, tidak dihitung di loop
* [ ] SR switch 44.1/48/96k konsisten
* [ ] Single-writer terjaga
* [ ] No NaN/Inf/denormal
* [ ] Latency report benar
* [ ] Clamp & constraint jalan

---

## 📂 Repo Structure

* [`HYGIENE.md`](./HYGIENE.md) → Rulebook penuh
* [`PARAMS.md`](./PARAMS.md) → Registry semua param
* [`CHANGELOG.md`](./CHANGELOG.md) → Catatan versi

---

## 🔎 Keywords

`DSP` · `JSFX` · `JUCE` · `Audio Plugin` · `Portability` · `Hygiene` · `Guardrails` · `Infinites Studio`

---

## 🔗 License

Bebas dipakai internal/eksternal.
🚫 **Jangan ubah guardrails inti** tanpa konsensus tim.

---
