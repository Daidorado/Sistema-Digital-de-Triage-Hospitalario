# TRIAGE DIGITAL

**Sistema de Triage Manchester para Guardia Hospitalaria**  
Guardia de Urgencias · v10.6 · 2026
Desarrollado por **Lic. Daiana Dorado**

---

## ¿Qué es?

TRIAGE DIGITAL es una aplicación web que digitaliza el proceso de triage de guardia siguiendo el **Manchester Triage System (MTS)**. Funciona completamente en el navegador, sin instalación ni base de datos externa, y está diseñada para operar desde cualquier dispositivo — computadora, tablet o celular.

Permite que múltiples roles del equipo de guardia (admisión, enfermería, médicos, jefatura) trabajen sobre la misma cola de pacientes en tiempo real, cada uno con acceso a las funciones que le corresponden.

---

## Demo en vivo

🔗 [daidorado.github.io/Sistema-Digital-de-Triage-Hospitalario](https://daidorado.github.io/Sistema-Digital-de-Triage-Hospitalario)

> Acceso libre sin contraseña. Seleccioná un rol e ingresá tu nombre para explorar el sistema.

---

## Funcionalidades

### Gestión de pacientes
- Registro de ingreso con datos completos (nombre, DNI, HC, edad, sexo, obra social)
- Cola de triage ordenada por prioridad y tiempo de espera
- Cambio de prioridad con motivo obligatorio y trazabilidad completa
- Re-triage con historial de clasificaciones por episodio

### Triage Manchester completo
- 53 motivos de consulta con discriminadores automáticos
- Clasificación por 5 colores: Rojo / Naranja / Amarillo / Verde / Azul
- Cronómetro Manchester por paciente con alerta visual al superar el tiempo objetivo

### Signos vitales y evaluación clínica
- FC, FR, TA, SpO₂, Temperatura, Glucemia, Pico Flujo
- Escala EVA (dolor 0–10) con colorización automática
- Glasgow simplificado (Alerta / Confuso / Somnoliento / No responde)
- Antecedentes Patológicos (APP): HTA, DBT, Cardiopatía, Asmático, Pte. Renal, Epiléptico, Anticoagulado, Alergia, Úlcera Estomacal, Psiquiátrico

### Protocolo de medicación — Prioridad Amarillo
Se activa automáticamente cuando EVA es 5, 6 o 7, o cuando la temperatura supera 38.5°C:

**Adultos** — grilla de 4 medicamentos:
| Medicamento | Dosis | Vía |
|-------------|-------|-----|
| Paracetamol | 1 g | V.O. |
| Naproxeno | 500 mg | V.O. |
| Ketorolaco | 20 mg | V.O. |
| Ketorolaco | 10 mg | S.L. |

> Si el paciente tiene Alergia, Úlcera Estomacal, Insuf. Renal o Anticoagulado marcado en APP, los AINES se bloquean automáticamente. Solo Paracetamol queda habilitado.

**Pediátrico** — selector en dos pasos:
- Presentación: Gotas 10% (hasta 2 años) o Jarabe 120 mg/5 mL (2–11 años)
- Rango de peso/edad → dosis exacta del protocolo

### Vista médica
- Lista de pacientes con triage completado, ordenados por color Manchester y tiempo
- Panel clínico completo: signos vitales con KPIs visuales, historial de triage, APP y medicación
- Registro de conducta: Alta, Internación, Derivación, Observación, Receta, Turno programado
- Nota médica libre y cierre de episodio

### Tablero EN VIVO (sin login)
- Contadores por color Manchester en tiempo real
- Lista de pacientes activos con estado y tiempo
- Actualización automática cada 10 segundos
- Disponible para cualquier servicio del hospital (Rayos, Laboratorio, Farmacia) sin necesidad de identificarse

### Buscador global
- Botón 🔍 BUSCAR siempre visible en el header
- Búsqueda por nombre, DNI, HC o motivo de consulta
- Navega directamente a la vista correspondiente del paciente

### Tablero de indicadores
- Métricas por turno activo (Mañana 07:00–18:59 / Noche 19:00–06:59)
- Distribución por color Manchester, tiempos promedio, motivos más frecuentes
- Detección automática de turno por timezone America/Argentina/Buenos_Aires

### Roles y permisos
| Rol | Acceso |
|-----|--------|
| Admisión | Ingreso de pacientes |
| Enfermería Triage | Triage completo, signos vitales, medicación protocolo |
| Médico (Clínica / Cirugía / Traumatología / Guardia) | Vista médica, conducta, cierre de episodio |
| Administrativo | Cola general, tablero, ingreso |
| Jefe de Guardia | Vista completa en modo lectura |
| Admin Sistema | Acceso total |

### Log y trazabilidad
- Registro cronológico de todas las acciones por episodio
- Trazabilidad completa con usuario, timestamp y descripción
- Historial de re-triajes por paciente

---

## Tecnología

| Componente | Detalle |
|------------|---------|
| Frontend | HTML5 · CSS3 · JavaScript vanilla (sin frameworks) |
| Tipografías | Bebas Neue · IBM Plex Mono · IBM Plex Sans (Google Fonts) |
| Datos | En memoria del navegador (localStorage no requerido) |
| PWA | Instalable en dispositivos móviles via Chrome/Edge |
| Deployment | GitHub Pages (static) · compatible con cualquier servidor web |
| Backend (próxima fase) | Flask + SQLAlchemy + PostgreSQL |

La aplicación es un **archivo HTML único** (`index.html`) sin dependencias externas de runtime. Todo el CSS, JavaScript y la lógica clínica están embebidos en el mismo archivo.

---

## Estructura del repositorio
```
/
├── index.html          # Aplicación completa (todo en un archivo)
└── README.md           # Este archivo
```

---

## Instalación y uso

### Opción 1 — Uso directo (más simple)
Abrir `index.html` en cualquier navegador moderno. No requiere servidor ni instalación.

### Opción 2 — Servidor local
```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .
```
Abrir `http://localhost:8080` en el navegador.

### Opción 3 — GitHub Pages (deploy en 1 minuto)
1. Hacer fork de este repositorio
2. Ir a Settings → Pages
3. Branch: main · Folder: / (root) → Save

---

## Compatibilidad

| Navegador | Versión mínima |
|-----------|---------------|
| Chrome / Edge | 90+ |
| Firefox | 88+ |
| Safari | 14+ |

- Responsive: pantallas desde 360px (celular) hasta 4K
- Instalable como PWA en Android e iOS
- Funciona sin conexión a internet si se despliega en red local

---

## Consideraciones clínicas

> Este sistema es una **herramienta de apoyo** al triage y no reemplaza el criterio clínico del profesional de salud. Toda decisión clínica es responsabilidad del profesional interviniente.

El protocolo de medicación fue desarrollado como referencia clínica para el diseño de las funcionalidades del sistema.

---

## Estado del proyecto

| Módulo | Estado |
|--------|--------|
| Triage Manchester (53 motivos) | ✅ Producción |
| Signos vitales y APP | ✅ Producción |
| Protocolo de medicación Amarillo | ✅ Producción |
| Vista médica y conductas | ✅ Producción |
| Tablero EN VIVO | ✅ Producción |
| Buscador global | ✅ Producción |
| PWA (instalable) | ✅ Producción |
| Backend Flask + PostgreSQL | 🔄 En desarrollo |
| Integración HIS | 🔄 En desarrollo |
| Autenticación con contraseña | 📋 Planificado |
| Modo offline completo | 📋 Planificado |

---

## Próxima fase

- **Backend persistente**: Flask + SQLAlchemy + PostgreSQL para guardar datos entre sesiones y compartir la cola entre múltiples dispositivos en red simultáneamente
- **Integración HIS**: conexión con el sistema de gestión hospitalaria institucional para importar datos de pacientes automáticamente
- **Autenticación**: acceso por usuario y contraseña con roles gestionados desde administración

---

## Autoría

Desarrollado íntegramente por **Lic. Daiana M. Dorado** — Licenciada en Enfermería con experiencia en urgencias, UTI e internado y estudiante de Tecnicatura en IA y Ciencias de Datos. Obra registrada ante la Dirección Nacional del Derecho de Autor (Argentina).
> Registro de Propiedad Intelectual — DNDA  
> Expediente EX-2026-25465614-APN-DNDA#MJ · Autoría: Lic. Daiana M. Dorado · 2026
---

## Licencia

Proyecto personal de portfolio — Lic. Daiana M. Dorado · 2026

---

**TRIAGE DIGITAL** · Lic. Daiana M. Dorado · 2026
