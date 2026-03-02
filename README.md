🏥 Sistema Digital de Triage Hospitalario
MVP Funcional · Google Sheets + Apps Script · 2024–2025

Desarrollado de forma autónoma por Daiana M. Dorado — Licenciada en Enfermería
Hospital de Urgencias, Córdoba, Argentina


📋 Descripción
Sistema digital de gestión de guardia hospitalaria que digitaliza y automatiza el flujo completo de triage, desde el registro del paciente hasta el cierre de la atención médica.
Diseñado por una profesional clínica con conocimiento directo del protocolo Manchester, el sistema reemplaza el registro en papel por una estructura de datos relacional que permite trazabilidad en tiempo real, priorización automática por gravedad y visualización de métricas operativas.
Problema que resuelve:

Falta de trazabilidad en el flujo de pacientes de guardia
Registro manual propenso a errores y pérdida de información
Ausencia de métricas operativas para la toma de decisiones clínicas


⚙️ Cómo funciona — Arquitectura
El sistema está construido sobre Google Sheets como base de datos relacional con automatización via Google Apps Script.
Estructura de tablas
┌─────────────────┐     ┌─────────────────┐
│    INGRESOS     │────▶│     TRIAGE      │
│  (registro QR)  │     │ (clasificación) │
└─────────────────┘     └────────┬────────┘
                                 │
                    ┌────────────▼────────┐
                    │       MEDICO        │
                    │  (atención clínica) │
                    └────────────┬────────┘
                                 │
                    ┌────────────▼────────┐
                    │    LOG_EVENTOS      │
                    │ (auditoría completa)│
                    └─────────────────────┘
Flujo de estados
Registro QR → Espera Triage → En Triage → Espera Médico → En Atención → Cerrado
Cada cambio de estado dispara un trigger onEdit que registra timestamp, usuario y datos clínicos en LOG_EVENTOS.
Componentes principales
ComponenteTecnologíaFunciónFormulario de ingresoGoogle Forms + QRRegistro de pretriage sin contactoMotor de automatizaciónGoogle Apps ScriptTriggers, lógica condicional, cambios de estadoBase de datosGoogle Sheets (4 tablas)Almacenamiento relacional de eventos clínicosDashboardGoogle Sheets + fórmulasKPIs, semáforo Manchester, tiempos de esperaPrototipo webHTMLInterfaz experimental para futura migraciónIntegración HISLógica por IDVinculación con sistema EcHos por historia clínica

📸 Capturas / Demo

🔧 Sección en construcción — próximamente se agregarán capturas del dashboard, formulario QR y vista de cola de espera.

Para una demo del sistema, podés contactarme en: doradodai65@gmail.com

🛠️ Stack Tecnológico
Google Sheets        → Estructura relacional tipo base de datos
Google Apps Script   → JavaScript server-side, automatización
Triggers onEdit      → Respuesta automática a cambios de estado
QUERY / FILTER       → Consultas dinámicas entre tablas
HTML                 → Prototipo de interfaz web
Conceptos SQL        → Diseño de arquitectura preparada para migración
EcHos (HIS)          → Integración lógica por ID de historia clínica

🗺️ Próximos pasos — Roadmap
v1.1 — Corto plazo

 Agregar autenticación por rol (enfermero / médico / administrativo)
 Exportación de reportes diarios en PDF
 Notificaciones automáticas por tiempo de espera excedido

v2.0 — Migración web

 Migrar base de datos a PostgreSQL o Supabase
 Desarrollar frontend en React o framework similar
 API REST para integración nativa con EcHos
 App móvil para registro de pretriage desde dispositivos del hospital

v3.0 — Inteligencia clínica

 Modelo predictivo de demanda por franja horaria
 Alertas automáticas por patrones de gravedad
 Integración con expediente clínico electrónico completo


👩‍⚕️ Autora
Daiana M. Dorado
Licenciada en Enfermería · Universidad Católica de Córdoba (2025)
Cursando: Inteligencia Artificial y Ciencias de Datos · Instituto Superior Santo Domingo
📍 Córdoba, Argentina
📧 doradodai65@gmail.com

📄 Licencia
Este proyecto es de uso educativo y profesional.
Desarrollado en contexto hospitalario real — datos clínicos anonimizados.

"Construido desde adentro del sistema de salud, para mejorarlo."
