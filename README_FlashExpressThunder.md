# Flash Express Thunder – Tu paquete en minutos

**Demo Offline Flutter App + Guía para compilar APK en la nube (GitHub Actions)**  
Mercado inicial: **Bolivia**  
Branding: Amarillo (#FFD500) / Negro (#000000)

---

## Tabla de Contenidos
1. [Qué es Flash Express Thunder](#qué-es-flash-express-thunder)
2. [Características de la Demo Offline](#características-de-la-demo-offline)
3. [Arquitectura futura](#arquitectura-futura)
4. [Modelo de negocio](#modelo-de-negocio)
5. [Requisitos previos](#requisitos-previos)
6. [Guía rápida: Compilar APK con GitHub Actions](#guía-rápida-compilar-apk-con-github-actions)
7. [Pasos detallados con capturas](#pasos-detallados-con-capturas)
8. [Instalar el APK en tu celular](#instalar-el-apk-en-tu-celular)
9. [Roadmap de Fases](#roadmap-de-fases)
10. [Contacto](#contacto)

---

## Qué es Flash Express Thunder
**Flash Express Thunder** es una plataforma de **paquetería express puerta a puerta** enfocada en velocidad, transparencia y libertad de precio. Los clientes publican envíos, proponen tarifa, y los repartidores responden con contraofertas (modelo tipo *InDriver*). Una vez aceptado, el cliente rastrea el envío en tiempo real y califica la experiencia.

---

## Características de la Demo Offline
Esta versión **NO requiere servidor**. Sirve para:
- Presentaciones a socios e inversionistas
- Validar flujo de usuario
- Demostrar experiencia visual tipo app real

Incluye:
- Splash + Branding
- Login rápido (Cliente / Repartidor)
- Crear envío (origen, destino, paquete, oferta)
- Ofertas simuladas de repartidores
- Tracking animado en mapa simulado de Bolivia
- Calificación post-entrega
- Historial
- Menú oculto para cambiar de rol

---

## Arquitectura futura
Cuando pasemos a producción:
- **Frontend:** Flutter (Android/iOS/Web)
- **Backend:** NestJS (Node + TypeScript)
- **BD:** PostgreSQL + Redis (colaboración en tiempo real)
- **Realtime Tracking:** WebSockets + GPS móvil
- **Chat Cliente ↔ Repartidor:** Mensajería push + notificaciones
- **Pagos:** Suscripción repartidores + pasarelas locales

---

## Modelo de negocio
Ingresos principales:
- **Suscripción mensual de repartidores** (ej. Bs. 35/mes)
- Planes escalables: Básico, Pro (más carreras, estadísticas, prioridad)
- Add-ons en futuro: Seguro de envío, prioridad en mapa, tarifas dinámicas

### Proyección simple (ejemplo)
| Repartidores activos | Cuota mensual (Bs.) | Ingreso mensual (Bs.) | Ingreso USD aprox* |
|---|---|---|---|
| 500 | 35 | 17,500 | ~2,500 |
| 1,000 | 35 | 35,000 | ~5,000 |
| 5,000 | 30 (volumen) | 150,000 | ~21,500 |

*Estimado USD calculado ~6.99 Bs/USD (ajustar según tipo de cambio).

---

## Requisitos previos
- Cuenta GitHub (gratuita)
- Navegador en celular
- Archivos del proyecto (carpeta Flutter)
- Conexión a internet

---

## Guía rápida: Compilar APK con GitHub Actions

**TL;DR:**
1. Crear repo en GitHub.
2. Subir código del proyecto.
3. Crear workflow `build_apk.yml`.
4. Run workflow.
5. Descargar `app-debug.apk`.

---

## Pasos detallados con capturas

### 1. Crear repositorio
![Crear repo](docs/img/step1_create_repo.png)

- Botón **+** → New Repository
- Nombre: `flash-express-thunder`
- Público → Create

### 2. Subir archivos
![Subir archivos](docs/img/step2_upload.png)

- Add file → Upload files
- Arrastra carpetas del proyecto
- Commit

### 3. Crear workflow
![Workflow](docs/img/step3_workflow.png)

Crea ruta: `.github/workflows/build_apk.yml` con:

```yaml
name: Build Flutter APK

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.7.0'
      - run: flutter pub get
      - run: flutter build apk --debug
      - uses: actions/upload-artifact@v3
        with:
          name: app-debug.apk
          path: build/app/outputs/flutter-apk/app-debug.apk
```

Commit.

### 4. Ejecutar build
- Ir a pestaña **Actions**
- Elegir workflow → **Run workflow**
- Esperar compilación (6-10 min)

### 5. Descargar APK
![Descargar artefacto](docs/img/step4_download_artifact.png)

- Abre build completado
- Sección *Artifacts*
- Descargar `app-debug.apk`

---

## Instalar el APK en tu celular

1. Descarga el archivo desde GitHub al teléfono.
2. Si aparece bloqueo, ve a **Ajustes → Seguridad → Instalar apps desconocidas** y habilita para tu navegador.
3. Abre el archivo → Instalar.
4. Busca **Flash Express Thunder** en tu lista de apps.

---

## Roadmap de Fases

### Fase 1 – Demo Offline (ESTA)
- Flujo completo sin servidor
- Presentación a inversionistas
- Validar UX

### Fase 2 – MVP Conectado
- Backend NestJS
- Registro persistente
- GPS en tiempo real
- Chat en vivo
- Suscripción repartidores

### Fase 3 – Escala Regional
- Optimización rutas
- Pagos locales + tarjetas
- Programar envíos
- Integración comercios B2B

---

## Contacto
**Proyecto:** Flash Express Thunder  
**Pitch:** Paquetería express Bolivia con negociación de precio y tracking en tiempo real.  
Contacto: *(agrega aquí tu correo o WhatsApp de negocios)*

---

### Licencia
Demo interna. No distribuir sin autorización del propietario del proyecto.
