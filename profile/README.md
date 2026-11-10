# Terraquipu 🌾🛰️

> **Sistema de Inteligencia Territorial y Regeneración Edáfica en los Andes**  
> *Desarrollado para el NASA Space Apps Challenge*

[![Live Demo](https://img.shields.io/badge/Demo%20en%20Vivo-GitHub%20Pages-22c55e?style=for-the-badge&logo=github)](https://terraquipu.github.io/terraquipu-web/)
[![Status](https://img.shields.io/badge/Producci%C3%B3n-Online%20(200%20OK)-0284c7?style=for-the-badge)](https://terraquipu.github.io/terraquipu-web/)

👉 **Acceso directo a la plataforma en producción:** [https://terraquipu.github.io/terraquipu-web/](https://terraquipu.github.io/terraquipu-web/)

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
| **Ing. Software IoT / Telemetría** | Emulación de Sensores Arduino y Telemetría de Campo | [`terraquipu-iot`](https://github.com/TerraQuipu/terraquipu-iot) | Emulador de datos de sensores Arduino (`mock_telemetry.py`) y streaming de telemetría de suelo (100% Software). |
| **Sistemas 1** | Geo-Backend & Base de Datos Espacial | [`terraquipu-api`](https://github.com/TerraQuipu/terraquipu-api) | API REST en FastAPI con PostGIS, ingesta de telemetría y endpoints de diagnóstico territorial. |
| **Sistemas 2** (`@alinafernanda77-ux`) | Frontend GIS & Experiencia de Usuario (UX) | [`terraquipu-web`](https://github.com/TerraQuipu/terraquipu-web) | Mapa interactivo 2D/3D, selector de parcelas y visualizador temporal de secuencias de rotación. |
| **Sistemas 3** | IA Explicativa (RAG) & Pitch Lead | [`terraquipu-api`](https://github.com/TerraQuipu/terraquipu-api) | Agente RAG que cita manuales técnicos oficiales de INIA/SENAMHI y estructura del pitch/video. |

---

## 🏛️ Arquitectura del Ecosistema

```mermaid
graph TD
    subgraph Macro ["Capa Macro (NASA Satelital)"]
        M1["NASA POWER / GPM - Precipitación"]
        M2["NASA SMAP - Humedad Regional"]
    end

    subgraph Meso ["Capa Meso (Topografía y Suelo)"]
        S1["NASA SRTM DEM 30m - Pendiente y Altitud"]
        S2["ISRIC SoilGrids 250m - pH, SOC, N"]
    end

    subgraph Micro ["Capa Micro (Terreno)"]
        IOT["Nodo IoT ESP32 - Ground Truth"]
    end

    subgraph Core ["Núcleo Terraquipu"]
        API["Terraquipu API (FastAPI + PostGIS)"]
        DATA["Terraquipu Data (Matriz INIA/SENAMHI)"]
        RAG["Capa Explicativa RAG (Embeddings INIA)"]
    end

    subgraph App ["Presentación"]
        WEB["Terraquipu Web (Dashboard GIS & Rotación)"]
    end

    M1 --> API
    M2 --> API
    S1 --> API
    S2 --> API
    IOT --> API
    DATA --> API
    API --> RAG
    API --> WEB
    RAG --> WEB
```

---

## 📦 Repositorios de la Organización

* [**`terraquipu-web`**](https://github.com/TerraQuipu/terraquipu-web) — [🌐 **Ver Demo en Vivo (Producción)**](https://terraquipu.github.io/terraquipu-web/): Dashboard interactivo en Next.js/React con mapas geoespaciales y visualizador de rotación multianual.
* [**`terraquipu-api`**](https://github.com/TerraQuipu/terraquipu-api): API geoespacial con FastAPI, base de datos PostGIS, motor de cálculo determinista y agente RAG.
* [**`terraquipu-data`**](https://github.com/TerraQuipu/terraquipu-data): Scripts de extracción satelital (NASA POWER, SoilGrids) y matriz agronómica validada (`crop_matrix.json`).
* [**`terraquipu-iot`**](https://github.com/TerraQuipu/terraquipu-iot): Emulador de telemetría de sensores Arduino/ESP32 y streaming de datos edáficos en tiempo real (100% Software).
* [**`.github`**](https://github.com/TerraQuipu/.github): Índice maestro, especificación técnica de contratos JSON y perfil institucional.
