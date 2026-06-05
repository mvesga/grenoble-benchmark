# Benchmark · Asistencia Psicológica TDAH+TSA · Grenoble + Bogotá

Guía comparativa de recursos terapéuticos en Grenoble (Francia) y Bogotá (Colombia) para pacientes con TDAH y Trastorno del Espectro Autista (TSA). Incluye sector público, privado, opciones en español, reseñas de pacientes, derechos sociales e intervención familiar para residentes permanentes en ambos países.

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

1. **Crear repositorio público** en [github.com/new](https://github.com/new)
   - Nombre sugerido: `grenoble-benchmark`
   - Visibilidad: **Public** *(el cifrado protege el contenido aunque el repo sea público)*

2. **Subir los archivos** (solo `index.html` y `README.md` son necesarios):
   ```bash
   git init
   git add index.html README.md
   git commit -m "Initial commit"
   git remote add origin https://github.com/TU_USUARIO/grenoble-benchmark.git
   git branch -M main
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

5. **Para actualizar** tras cambios en el benchmark:
   ```bash
   cd ~/Desktop/grenoble-benchmark
   cp ~/Downloads/index.html .
   git add index.html
   git commit -m "Update benchmark"
   git push
   ```

> ⚠️ GitHub Pages publica el sitio públicamente aunque el repo sea público.  
> La contraseña cifra el contenido — nadie puede leerlo sin ella, incluso con acceso a la URL.

---

## 🔑 Cambiar la contraseña

Necesitas Python 3 con la librería `cryptography`:

```bash
pip install cryptography
```

Luego ejecuta este script apuntando al HTML original y tu nueva contraseña:

```python
import os, base64, hashlib, re
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

with open(OUTPUT_HTML, 'r') as f:
    shell = f.read()

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
| Repositorio | Público en GitHub — el payload cifrado no es útil sin la contraseña |

> El contenido descifrado **no se guarda** en ningún lado — desaparece al cerrar la pestaña.

---

## 📋 Contenido del benchmark

### 🇫🇷 Grenoble, Francia
- **Sector público:** CHU Grenoble TSA Adulte, CHAI Centre Expert TSA, Centre Expert Fondamental, CMP Adulte
- **Sector privado:** 8 especialistas con tarifas, disponibilidad y datos de contacto
- **🇪🇸 En español:** Psy'sère (Rocío Roure, neuropsicóloga TSA/TDAH adultos) y psicóloga bilingüe
- **Derechos sociales:** PUMa, Mon Soutien Psy, MDPH, C2S, PCO, RQTH
- **Marco legal familiar:** Habilitation familiale, curatelle/tutelle, rol del aidant

### 🇨🇴 Bogotá, Colombia
- **Sistema público:** Ruta EPS (PBS), hospitales universitarios (HUSI, San Ignacio, U. Nacional)
- **Sector privado:** 6 especialistas con reseñas verificadas de Doctoralia y Top Doctors
- **Reseñas de pacientes:** calificaciones y número de opiniones reales por especialista
- **Derechos:** EPS/PBS, Ley 1616 Salud Mental, Ley 1618 Discapacidad, tutela, prepagadas
- **Marco legal familiar:** Ley 1996/2019 (apoyos, eliminación de interdicción), tutela en salud

### Filtros interactivos
- 🗂 **Tipo:** Público · Privado · TDAH · TSA · 🇪🇸 Español
- ⏱ **Espera:** Rápida (<4 sem) · Media (1–6 m) · Larga (>6 m)
- 💶 **Costo:** Gratuito · Reembolso parcial · Solo privado
- ⭐ **Reseñas:** Con reseñas verificadas · Mejor calificadas (4.8+)

---

*Datos orientativos · 2025-2026 · Verificar disponibilidad y precios directamente con cada profesional.*
