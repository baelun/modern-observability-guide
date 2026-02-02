# Modern Observability Guide/Practice

A hands-on practice project for modern observability stack: Prometheus, Grafana, Loki, and Grafana Alloy.

這是一個現代可觀測性技術棧的實作練習專案：Prometheus、Grafana、Loki 和 Grafana Alloy。

---

## Architecture / 架構

```
┌─────────────────┐     ┌─────────────────┐
│  Node Exporter  │────▶│                 │
│    (metrics)    │     │                 │
└─────────────────┘     │                 │
                        │  Grafana Alloy  │────▶ Prometheus
┌─────────────────┐     │   (collector)   │
│   /var/log/*    │────▶│                 │────▶ Loki
│     (logs)      │     │                 │
└─────────────────┘     └─────────────────┘
                                │
                                ▼
                        ┌─────────────────┐
                        │     Grafana     │
                        │  (visualization)│
                        └─────────────────┘
```

## Components / 元件

| Service | Port | Description |
|---------|------|-------------|
| Grafana | 9010 | Dashboard & visualization / 儀表板與視覺化 |
| Prometheus | 9090 | Metrics storage / 指標儲存 |
| Loki | 3100 | Log aggregation / 日誌聚合 |
| Alloy | - | Telemetry collector / 遙測收集器 |
| Node Exporter | 9100 | System metrics / 系統指標 |
| Alertmanager | 9012 | Alert handling / 告警處理 |

## Quick Start / 快速開始

```bash
cd docker
docker compose up -d
```

Access Grafana at `http://localhost:9010`
- Username: `admin`
- Password: `1qaz2wsx3edc`

開啟 Grafana：`http://localhost:9010`
- 帳號：`admin`
- 密碼：`1qaz2wsx3edc`

## Project Structure / 專案結構

```
.
├── docker/
│   ├── docker-compose.yml    # Main compose file / 主要 compose 檔
│   └── volume/
│       ├── alloy/
│       │   └── config.alloy  # Alloy config / Alloy 設定
│       ├── loki/
│       │   └── loki-config.yaml
│       └── grafana/
└── .devcontainer/            # Dev container config / 開發容器設定
```


## What's Collected / 收集內容

**Metrics / 指標：**
- Node Exporter: CPU, memory, disk, network
- cAdvisor: Container metrics (commented out / 已註解)
- ClickHouse: Database metrics (if available / 如有)

**Logs / 日誌：**
- `/var/log/syslog`

## License

Apache License 2.0
