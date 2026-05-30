# 🌐 AuraTrack: Edge-AI Offline Tracking Architecture

A decentralized, zero-network location tracking and predictive mapping ecosystem powered by edge AI, LoRa telemetry, and local spatial databases. Built for disaster response and deep-wilderness operations where cellular and cloud infrastructure has failed.

**Team:** Rifat & Galib
**Status:** Architectural Phase & Prototyping

---

## 🏗️ System Architecture

AuraTrack decouples tracking from the cloud using a highly resilient 3-tier offline stack:

1. **Edge Hardware:** Field agents equipped with ESP32 + GNSS + LoRa SX1278.
2. **Base Station Ingestion:** Local Python serial daemon fetching encrypted 12-byte payload strings.
3. **Command UI:** Offline Next.js dashboard utilizing MapLibre GL JS and local `.mbtiles`.

```mermaid
graph TD
    subgraph Edge Layer
        A[ESP32 Microcontroller] -->|GNSS Data| B(Compress to 12-byte Payload)
        B -->|LoRa 868/915MHz| C((LoRa Receiver))
    end

    subgraph Base Station Ingestion
        C -->|USB/Serial| D[Python pyserial Daemon]
        D -->|Unpack & Validate via Pydantic| E[(PostgreSQL + PostGIS)]
    end

    subgraph Visualization Engine
        E -->|FastAPI REST/WebSockets| F[Next.js Command Dashboard]
        G[(Local .mbtiles SQLite)] -->|Vector Maps| F
    end
📂 Production Folder Structure
This repository outlines the planned monolithic structure for the build phase:
