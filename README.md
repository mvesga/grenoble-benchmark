# Benchmark TDAH+TSA · Grenoble + Bogotá + Sabana Norte

Dos guías comparativas de recursos para adultos con TDAH y Trastorno del Espectro Autista (TSA), cubriendo Grenoble (Francia), Bogotá y Sabana Norte / Chía-Cajicá (Colombia).

---

## 📄 Dos benchmarks, dos archivos publicados

| Archivo publicado | Contenido | Fuente sin cifrar |
|---|---|---|
| `index.html` | Especialistas psicológicos (TCC/TCCE) · Grenoble + Bogotá | `grenoble-tdah-tsa-benchmark.html` |
| `index-lifecoach.html` | Acompañamiento domiciliario · Grenoble + Bogotá + Sabana Norte | `lifecoach-tdah-tsa-benchmark.html` |

---

## 🔐 Acceso

Ambos archivos están cifrados con la misma contraseña (AES-256-GCM en cliente).
**Contraseña:** `grenoble2025` ← cámbiala antes de compartir (ver instrucciones abajo)

---

## 🚀 Publicar / actualizar en GitHub Pages

### Primera vez

```bash
git init
git add index.html index-lifecoach.html README.md
git commit -m "Initial commit"
git remote add origin https://github.com/TU_USUARIO/grenoble-benchmark.git
git branch -M main
git push -u origin main
```

Activar GitHub Pages: **Settings → Pages → Branch: main / root → Save**

URLs resultantes:
```
https://TU_USUARIO.github.io/grenoble-benchmark/              ← benchmark psicológico
https://TU_USUARIO.github.io/grenoble-benchmark/index-lifecoach.html  ← acompañamiento
```

### Actualizar tras cambios

```bash
cd ~/Desktop/grenoble-benchmark
cp ~/Downloads/index.html .               # benchmark psicológico actualizado
cp ~/Downloads/index-lifecoach.html .     # benchmark lifecoach actualizado
cp ~/Downloads/README.md .
git add index.html index-lifecoach.html README.md
git commit -m "Update benchmarks - $(date +%Y-%m-%d)"
git push
```

> ⚠️ El repo es público pero el contenido está cifrado — nadie puede leerlo sin la contraseña.

---

## 🔑 Cambiar la contraseña

Necesitas Python 3 con la librería `cryptography` (`pip install cryptography`).

```python
import os, base64, hashlib, re
from cryptography.hazmat.primitives.ciphers.aead import AESGCM

# ── Configura aquí ──────────────────────────────────────────────
SOURCE_HTML = "grenoble-tdah-tsa-benchmark.html"   # o lifecoach-tdah-tsa-benchmark.html
OUTPUT_HTML = "index.html"                          # o index-lifecoach.html
PASSWORD    = "tu-nueva-contraseña-segura"
# ────────────────────────────────────────────────────────────────

with open(SOURCE_HTML, 'rb') as f:
    plaintext = f.read()

salt = os.urandom(32)
iv   = os.urandom(12)
key  = hashlib.pbkdf2_hmac('sha256', PASSWORD.encode(), salt, 200000, dklen=32)
ciphertext = AESGCM(key).encrypt(iv, plaintext, None)
payload = base64.b64encode(salt + iv + ciphertext).decode()

with open(OUTPUT_HTML, 'r') as f:
    shell = f.read()

shell = re.sub(r'(const PAYLOAD_B64 = ")[^"]*(")', f'\\g<1>{payload}\\g<2>', shell)

with open(OUTPUT_HTML, 'w') as f:
    f.write(shell)

print(f"✅ {OUTPUT_HTML} actualizado")
```

Repite el proceso para cada archivo (psicológico y lifecoach) si cambias la contraseña.

---

## 🛡️ Seguridad

| Capa | Detalle |
|---|---|
| Cifrado | AES-256-GCM (cifrado autenticado) |
| KDF | PBKDF2-SHA256 · 200.000 iteraciones · salt aleatorio de 32 bytes |
| Ejecución | 100% en el navegador — el servidor nunca ve la contraseña ni el contenido |
| Repositorio | Público en GitHub — el payload cifrado es ilegible sin la contraseña |

> El contenido descifrado no se guarda en ningún lado — desaparece al cerrar la pestaña.

---

## 📋 Contenido

### `index.html` — Especialistas psicológicos (TCC/TCCE)

#### 🇫🇷 Grenoble, Francia
- Sector público: CHU Grenoble TSA Adulte, CHAI Centre Expert TSA, Centre Expert Fondamental, CMP Adulte
- Sector privado: 8 especialistas con tarifas, disponibilidad y contacto
- 🇪🇸 En español: Psy'sère (Rocío Roure) y psicóloga bilingüe
- Derechos: PUMa, Mon Soutien Psy, MDPH, C2S, PCO, RQTH
- Marco legal familiar: Habilitation familiale, curatelle/tutelle, rol del aidant

#### 🇨🇴 Bogotá, Colombia
- Sistema público: Ruta EPS (PBS), hospitales universitarios
- Sector privado: 6 especialistas con reseñas verificadas (Doctoralia / Top Doctors)
- Derechos: Ley 1616, Ley 1618, tutela, prepagadas
- Marco legal familiar: Ley 1996/2019, acuerdos de apoyo, eliminación de interdicción

#### Filtros
🗂 Tipo · ⏱ Espera · 💶 Costo · ⭐ Reseñas

---

### `index-lifecoach.html` — Acompañamiento domiciliario

#### 🇫🇷 Grenoble, Francia
- Ergoterapeutas a domicilio, coaches en neurodivergencia
- SAMSAH ALHPI Le Serdac (Sassenage, 18–60 años) y SAVS APAJH38 (Eybens, 18–60 años)
- Acompañantes terapéuticos, financiamiento PCH "soutien à l'autonomie"
- Entrada vía MDA Isère (15 av. Doyen Louis Weil, 04 38 12 48 48) → CDAPH

#### 🇨🇴 Bogotá, Colombia
- Terapeutas ocupacionales a domicilio, coaches neurodivergencia
- Ruta EPS para TO, prepagadas, particular

#### 🇨🇴 Sabana Norte — Chía / Cajicá
- Neurolearning Terapias (Km 1.5 Cajicá-Chía, sede física)
- Clínica Universidad de La Sabana (psiquiatría + TO + psicología)
- ESE Hospital de Chía (puerta de entrada EPS)
- Servicios a domicilio que cubren toda la Sabana Norte

#### Filtros
🗂 Tipo · ⏱ Espera · 💰 Costo · 🏠 Domicilio · 🔧 Función ejecutiva

---

*Datos orientativos · 2025-2026 · Verificar disponibilidad y precios directamente con cada profesional.*
