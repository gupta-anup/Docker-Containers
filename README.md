# Backend Developer's Docker Toolkit 🚀

A comprehensive collection of Docker Compose setups for popular backend development tools.

## 🛠️ Available Tools

### **Databases**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **MySQL** | 3306 | phpMyAdmin (8081) | root/rootpassword |
| **PostgreSQL** | 5432 | pgAdmin (8082) | admin@admin.com/admin |
| **MongoDB** | 27017 | Mongo Express (8084) | admin/admin123 |
| **Redis** | 6379 | Redis Commander (8083) | password: redispassword |

### **Message Queues**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **Kafka** | 9092 | Kafka UI (8080) | - |
| **RabbitMQ** | 5672 | Management UI (15672) | admin/admin123 |

### **Search & Analytics**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **OpenSearch** | 9200 | Dashboard (5601) | No auth (learning mode) |

### **Storage**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **MinIO** | 9000, 9001 | Console (9001) | minioadmin/minioadmin123 |

### **Monitoring & Observability**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **Prometheus** | 9090 | Prometheus UI (9090) | - |
| **Grafana** | 3000 | Grafana UI (3000) | admin/admin123 |
| **Jaeger** | 16686 | Jaeger UI (16686) | - |
| **Zipkin** | 9411 | Zipkin UI (9411) | - |

### **Development Tools**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **SonarQube** | 9000 | SonarQube UI (9000) | admin/admin |
| **Keycloak** | 8080 | Admin Console (8080) | admin/admin123 |

### **Infrastructure**
| Tool | Port(s) | Web UI | Default Credentials |
|------|---------|---------|-------------------|
| **Nginx** | 80, 443 | - | - |

## 🚀 Quick Start

### Start a specific service:
```bash
cd <tool-folder>
docker-compose up -d
```

### Start all services (from root directory):
```bash
# Start all databases
cd MySQL && docker-compose up -d && cd ..
cd PostgreSQL && docker-compose up -d && cd ..
cd MongoDB && docker-compose up -d && cd ..
cd Redis && docker-compose up -d && cd ..

# Start message queues
cd Kafka && docker-compose up -d && cd ..
cd RabbitMQ && docker-compose up -d && cd ..

# Start monitoring stack
cd Monitoring && docker-compose up -d && cd ..
```

### Stop services:
```bash
cd <tool-folder>
docker-compose down
```

### Remove data (reset):
```bash
cd <tool-folder>
docker-compose down -v
```

## 📋 Service Status Check

```bash
# Check all running containers
docker ps

# Check specific service logs
docker-compose logs -f <service-name>
```

## 🔧 Configuration Notes

### **For Production Use:**
1. **Change default passwords** in all compose files
2. **Enable SSL/TLS** where applicable
3. **Configure proper networking** and security groups
4. **Set up proper backup strategies**
5. **Configure resource limits**

### **Networking:**
- Each service runs in its own network for isolation
- Use service names for inter-container communication
- External ports are exposed for development access

### **Data Persistence:**
- All services use named volumes for data persistence
- Data survives container restarts
- Use `docker-compose down -v` to remove data

## 🎯 Common Use Cases

### **Microservices Development:**
- Kafka + PostgreSQL + Redis + Jaeger
- API Gateway: Nginx
- Identity: Keycloak

### **Data Pipeline:**
- Kafka + OpenSearch + MongoDB
- Monitoring: Prometheus + Grafana

### **Full Stack Development:**
- PostgreSQL/MySQL + Redis + RabbitMQ
- Code Quality: SonarQube
- Reverse Proxy: Nginx

## 🆘 Troubleshooting

### **Port Conflicts:**
If you get port conflicts, check which services are running:
```bash
netstat -an | findstr :3306  # Windows
ss -tulpn | grep :3306       # Linux/Mac
```

### **Memory Issues:**
Some services (like OpenSearch, SonarQube) require more memory:
```bash
# Increase Docker Desktop memory to at least 4GB
# Or reduce heap sizes in compose files
```

### **Permission Issues:**
On Linux/Mac, you might need to adjust volume permissions:
```bash
sudo chown -R $USER:$USER ./data
```

## 📝 Notes

- All services are configured for **development/learning** purposes
- **Security is disabled** or uses default credentials for ease of use
- **Always change credentials** before using in production
- Some services include web UIs for easier management
- Health checks are configured where applicable

Happy coding! 🎉
