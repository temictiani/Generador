# 🔐 Generador y analizador de contraseñas

Herramienta web ligera para **generar contraseñas seguras** y **analizar la fortaleza** de las que ya usas. Funciona 100 % en tu navegador, sin servidores, sin dependencias y sin guardar nada.

## ✨ Características

**Generador**
- Longitud configurable de 8 a 64 caracteres.
- Mayúsculas, minúsculas, números y símbolos a elección.
- Opción para evitar caracteres confusos (`0 O 1 l I`).
- Aleatoriedad criptográfica con `crypto.getRandomValues`.
- Copia al portapapeles con un toque.

**Analizador**
- Cálculo de entropía en bits y nivel de fortaleza.
- Estimación del tiempo de fuerza bruta.
- Detección de contraseñas comunes, secuencias (`1234`, `abcd`, `qwerty`) y caracteres repetidos.
- Lista de comprobaciones clara (✓ / ✗).
- Comprobación opcional de filtraciones con Have I Been Pwned (k-anonymity).

---

## 🧠 Cómo funciona

### Entropía

La fortaleza se mide en bits de entropía:

```
entropía = longitud × log₂(tamaño del conjunto de caracteres)
```

Cada bit extra duplica el número de intentos que necesita un atacante.

| Entropía | Nivel |
|----------|-------|
| < 28 bits | Muy débil |
| 28 – 35 bits | Débil |
| 36 – 59 bits | Media |
| 60 – 79 bits | Fuerte |
| ≥ 80 bits | Muy fuerte |

### Penalizaciones

Una contraseña larga no siempre es buena. El analizador resta puntos si detecta:
- Contraseñas del top de listas filtradas (`password1`, `123456`...).
- Secuencias de teclado o alfabeto de 4 o más caracteres.
- Tres o más caracteres iguales seguidos.
- Sustituciones tipo *leet* (`p@ssw0rd`).

### Tiempo estimado

Se asume un atacante con **10¹⁰ intentos por segundo** contra un hash rápido (escenario pesimista). Contra servicios en línea con límite de intentos, el tiempo real sería muchísimo mayor.

### Aleatoriedad segura

`Math.random()` **no** es seguro para contraseñas. Esta herramienta usa `crypto.getRandomValues` y muestreo por rechazo para evitar el sesgo de módulo, de modo que todos los caracteres tienen exactamente la misma probabilidad.

### Comprobación de filtraciones (k-anonymity)

Al pulsar **Comprobar filtraciones**:
1. Se calcula el hash SHA-1 de la contraseña en tu navegador.
2. Solo se envían los **primeros 5 caracteres** del hash a la API de [Have I Been Pwned](https://haveibeenpwned.com/API/v3#PwnedPasswords).
3. La coincidencia se busca localmente en la respuesta.

La contraseña nunca sale de tu dispositivo.

---

## 🚀 Uso

**Online:** abre la demo y listo.

**En local:**

```bash
git clone https://github.com/TU-USUARIO/Generador.git
cd Generador
# abre index.html en tu navegador, o sirve la carpeta:
python3 -m http.server 8000
```

Luego entra a `http://localhost:8000`.

**Desplegar tu propia copia:** haz un fork y activa *Settings → Pages → Deploy from a branch → main / root*.

---

## 🛡️ Privacidad y seguridad

- Todo el procesamiento es local.
- No se usan cookies, analíticas ni almacenamiento.
- La única petición externa es la comprobación de filtraciones, y solo si tú la activas.
- Aun así, para probar el analizador es mejor usar contraseñas *parecidas* a las tuyas y no las reales.

---

## ⚠️ Aviso de uso ético

Esta herramienta es **defensiva y educativa**. Está pensada para ayudarte a crear y evaluar contraseñas propias. No incluye ni debe usarse para ataques de fuerza bruta, robo de credenciales ni acceso no autorizado a cuentas ajenas.

---

## 🗺️ Roadmap

- [ ] Generador de frases de contraseña (*passphrases*).
- [ ] Modo claro / oscuro manual.
- [ ] Tests automatizados de la lógica de análisis.
- [ ] Versión en inglés.

---

## 🧰 Tecnologías

HTML5 · CSS3 · JavaScript (vanilla) · Web Crypto API · GitHub Pages

