# Benchmark · Asistencia Psicológica TDAH+TSA · Grenoble

Guía comparativa de recursos terapéuticos en Grenoble e Isère para pacientes con TDAH y Trastorno del Espectro Autista (TSA). Incluye sector público, privado, opciones en español, y derechos sociales para residentes permanentes en Francia.

---

## 🔐 Acceso

El sitio está protegido con contraseña (cifrado AES-256-GCM en cliente).  
**Contraseña:** `grenoble2025` ← cámbiala antes de compartir (ver instrucciones abajo)

---

## 📁 Archivos

| Archivo | Descripción |
|---|---|
| `index.html` | Página protegida con contraseña — la que se publica |
| `grenoble-tdah-tsa-benchmark.html` | Fuente original sin cifrar — **no publicar** |
| `README.md` | Este archivo |

---

## 🚀 Publicar en GitHub Pages

1. **Crear repositorio privado** en [github.com/new](https://github.com/new)
   - Nombre sugerido: `grenoble-benchmark`
   - Visibilidad: **Private**

2. **Subir los archivos** (solo `index.html` y `README.md` son necesarios):
   ```bash
   git init
   git add index.html README.md
   git commit -m "Initial commit"
   git remote add origin https://github.com/TU_USUARIO/grenoble-benchmark.git
   git push -u origin main
   ```

3. **Activar GitHub Pages:**
   - Ir a **Settings → Pages**
   - Source: `Deploy from a branch`
   - Branch: `main` / `/ (root)`
   - Guardar

4. El sitio estará disponible en:
   ```
   https://TU_USUARIO.github.io/grenoble-benchmark/
   ```

> ⚠️ GitHub Pages publica el sitio públicamente aunque el repo sea privado.  
> La contraseña cifra el contenido — nadie puede leerlo sin ella, incluso con acceso a la URL.

---

## 🔑 Cambiar la contraseña

Necesitas Python 3 con la librería `cryptography`:

```bash
pip install cryptography
```

Luego ejecuta este script apuntando al HTML original y tu nueva contraseña:

```python
import os, base64, hashlib
from cryptography.hazmat.primitives.ciphers.aead import AESGCM

# ── Configura aquí ──────────────────────────────────────────────
SOURCE_HTML = "grenoble-tdah-tsa-benchmark.html"   # fuente sin cifrar
OUTPUT_HTML = "index.html"                          # archivo a publicar
PASSWORD    = "tu-nueva-contraseña-segura"          # ← cámbiala
# ────────────────────────────────────────────────────────────────

with open(SOURCE_HTML, 'rb') as f:
    plaintext = f.read()

salt = os.urandom(32)
iv   = os.urandom(12)
key  = hashlib.pbkdf2_hmac('sha256', PASSWORD.encode(), salt, 200000, dklen=32)

ciphertext = AESGCM(key).encrypt(iv, plaintext, None)
payload    = base64.b64encode(salt + iv + ciphertext).decode()

# Lee la plantilla shell (index.html existente) y actualiza el payload
with open(OUTPUT_HTML, 'r') as f:
    shell = f.read()

# Reemplaza el payload entre las comillas de PAYLOAD_B64
import re
shell = re.sub(r'(const PAYLOAD_B64 = ")[^"]*(")', f'\\g<1>{payload}\\g<2>', shell)

with open(OUTPUT_HTML, 'w') as f:
    f.write(shell)

print(f"✅ {OUTPUT_HTML} actualizado con nueva contraseña")
```

---

## 🛡️ Seguridad

| Capa | Detalle |
|---|---|
| Cifrado | AES-256-GCM (cifrado autenticado) |
| KDF | PBKDF2-SHA256 · 200.000 iteraciones · salt aleatorio de 32 bytes |
| Ejecución | 100% en el navegador del cliente — el servidor no ve la contraseña ni el contenido |
| Repositorio | Privado en GitHub — el payload cifrado no es útil sin la contraseña |

> El contenido descifrado **no se guarda** en ningún lado — desaparece al cerrar la pestaña.

---

## 📋 Contenido del benchmark

- **Sector público:** CHU Grenoble TSA, CHAI Centre Expert, Centre Expert Fondamental, CMP Adulte
- **Sector privado:** 8 especialistas con tarifas, disponibilidad y datos de contacto
- **Filtros interactivos:** Tipo · Especialidad · Idioma · Tiempo de espera · Costo
- **Derechos sociales:** PUMa, Mon Soutien Psy, MDPH, C2S, PCO, RQTH
- **🇪🇸 En español:** Psy'sère (Rocío Roure) y psicóloga bilingüe en Grenoble

---

*Datos orientativos · 2025-2026 · Verificar disponibilidad y precios directamente con cada profesional.*
