# Terraquipu 🌾🛰️

> **Sistema de Inteligencia Territorial y Regeneración Edáfica en los Andes**  
> *Desarrollado para el NASA Space Apps Challenge*

---

## 🌎 Visión General

**Terraquipu** democratiza la inteligencia satelital de la NASA y la ciencia del suelo para transformar la **rotación de cultivos** en el escudo de resiliencia más poderoso de los agricultores andinos frente a eventos climáticos extremos como **El Niño**.

El sistema integra:
1. **Datos Satelitales de la NASA:** Observaciones de precipitación (GPM / NASA POWER), humedad de suelo (SMAP) y topografía de alta resolución (SRTM DEM 30m).
2. **Propiedades Edáficas (SoilGrids v2.0):** Diagnóstico geoespacial de pH, carbono orgánico y nitrógeno a 250m.
3. **Calibración In-Situ (Nodo IoT):** Estación de campo con ESP32 para corregir el sesgo satelital sobre el terreno.
4. **Motor Determinista + Agente Explicativo (RAG):** Cálculo matemático auditable basado en manuales de **INIA** y **SENAMHI** sin alucinaciones.

---

## 👥 Equipo Multidisciplinario y Roles (Sprint 48h)

| Integrante / Especialidad | Rol en el Proyecto | Repositorio Asignado | Entregable Clave |
| :--- | :--- | :--- | :--- |
| **Ing. Ambiental** | Modelado Agronómico y Salud del Suelo | [`terraquipu-data`](https://github.com/TerraQuipu/terraquipu-data) | Matriz agronómica andina (`crop_matrix.json`) con umbrales fenológicos y reglas de rotación. |
| **Ciencia de Datos** | Pipelines Satelitales y Scoring Multicriterio | [`terraquipu-data`](https://github.com/TerraQuipu/terraquipu-data) | Pipeline de extracción NASA POWER / SoilGrids y algoritmo determinista de idoneidad. |
| **Ing. Electrónico** | Hardware IoT y Ground-Truthing | [`terraquipu-iot`](https://github.com/TerraQuipu/terraquipu-iot) | Firmware ESP32 de telemetría in-situ y simulador de contingencia (`mock_telemetry.py`). |
| **Sistemas 1** | Geo-Backend & Base de Datos Espacial | [`terraquipu-api`](https://github.com/TerraQuipu/terraquipu-api) | API REST en FastAPI con PostGIS, ingesta de telemetría y endpoints de diagnóstico territorial. |
| **Sistemas 2** (`@alinafernanda77-ux`) | Frontend GIS & Experiencia de Usuario (UX) | [`terraquipu-web`](https://github.com/TerraQuipu/terraquipu-web) | Mapa interactivo 2D/3D, selector de parcelas y visualizador temporal de secuencias de rotación. |
| **Sistemas 3** | IA Explicativa (RAG) & Pitch Lead | [`terraquipu-api`](https://github.com/TerraQuipu/terraquipu-api) | Agente RAG que cita manuales técnicos oficiales de INIA/SENAMHI y estructura del pitch/video. |

---

## 🏛️ Arquitectura del Ecosistema

```mermaid
graph TD
    subgraph Capa Macro (NASA Satelital)
        M1[NASA POWER / GPM - Precipitación]
        M2[NASA SMAP - Humedad Regional]
    end

    subgraph Capa Meso (Topografía & Suelo)
        S1[NASA SRTM DEM 30m - Pendiente y Altitud]
        S2[ISRIC SoilGrids 250m - pH, SOC, N]
    end

    subgraph Capa Micro (Terreno)
        IOT[Nodo IoT ESP32 - Ground Truth]
    end

    M1 & M2 & S1 & S2 & IOT --> API[Terraquipu API - FastAPI + PostGIS]
    DATA[Terraquipu Data - Matriz INIA/SENAMHI] --> API
    API --> RAG[Capa Explicativa RAG - Embeddings INIA]
    API & RAG --> WEB[Terraquipu Web - Dashboard GIS & Rotación]
```

---

## 📦 Repositorios de la Organización

* [**`terraquipu-web`**](https://github.com/TerraQuipu/terraquipu-web): Dashboard interactivo en Next.js/React con mapas geoespaciales y visualizador de rotación multianual.
* [**`terraquipu-api`**](https://github.com/TerraQuipu/terraquipu-api): API geoespacial con FastAPI, base de datos PostGIS, motor de cálculo determinista y agente RAG.
* [**`terraquipu-data`**](https://github.com/TerraQuipu/terraquipu-data): Scripts de extracción satelital (NASA POWER, SoilGrids) y matriz agronómica validada (`crop_matrix.json`).
* [**`terraquipu-iot`**](https://github.com/TerraQuipu/terraquipu-iot): Firmware ESP32 para sensores capacitivos y script de contingencia `mock_telemetry.py`.
* [**`.github`**](https://github.com/TerraQuipu/.github): Índice maestro, especificación técnica de contratos JSON y perfil institucional.
