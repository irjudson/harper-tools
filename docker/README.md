# Harper Docker Stack

**What it is:** Ready-to-run Harper with Grafana monitoring.
**Why use it:** Switch between single and cluster modes without reconfiguration.

## Quick Start

### Single Node
```bash
docker-compose --profile single up -d
```

### 3-Node Cluster
```bash
docker-compose --profile cluster up -d
```

## Access Points

**Harper**
- Single/Node-0: http://localhost:9925
- Node-1: http://localhost:9935
- Node-2: http://localhost:9945
- Credentials: admin/HarperRocks!

**Grafana**
- URL: http://localhost:3000
- Credentials: admin/admin
- Dashboard: http://localhost:3000/d/harperdb-monitoring

![Grafana Dashboard](docs/single-instance-grafana.png)
*Harper metrics dashboard for a single instance*

## Project Files

```
.
├── docker-compose.yml          # Main config
├── .env.example               # Environment template
├── scripts/
│   └── setup-grafana.sh      # Auto-setup dashboard
├── data/                     # Container volumes (auto-created)
└── docs/                     # Documentation
```

## How It Works

1. **Consistent naming** - `harper-0` exists in both modes
2. **Same datasource** - Grafana always points to `harper-0:9925`
3. **Auto-provisioning** - Dashboards configured on startup
4. **No manual changes** - Switch modes freely

## Requirements

- Docker Compose 2.0+
- 4GB+ RAM for cluster
- Ports: 3000, 9925-9946

## Troubleshooting

```bash
# Clean restart
docker-compose down
docker-compose --profile single up -d
```

## Documentation

- [Usage Guide](USAGE_GUIDE.md)
- [Data Formats](docs/DATA-FORMAT-ANALYSIS.md)