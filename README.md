## File Structure
.
├── auth       
│   └── deploy           
│       ├── auth-config.yml         
│       └── auth.yaml          
├── chat        
│   └── deploy       
│       └── chat.yaml     
├── frontend   
│   └── front-deployment.yaml   
├── gateway   
│   └── deploy   
│       └── gateway.yml   
├── monitoring   
│   ├── get_helm.sh   
│   ├── grafana-external.yaml  
│   ├── grafana-ingress.yaml  
│   └── grafana-values.yaml   
├── network   
│   ├── certificate  
│   │   └── certificate.yaml  
│   ├── cluster-ip  
│   │   ├── auth-cluster-ip.yaml  
│   │   ├── chat-cluster-ip.yml  
│   │   ├── front-cluster-ip.yaml  
│   │   ├── gateway-cluster-ip.yaml  
│   │   ├── order-cluster-ip.yaml    
│   │   └── product-cluster-ip.yaml   
│   ├── control-center  
│   │   └── control-center.yml  
│   ├── health-check  
│   │   └── health.yaml  
│   └── ingress  
│       └── yoger-ingress.yml  
├── order  
│   └── deploy  
│       └── order.yaml  
└── product  
    └── deploy  
        └── product.yaml  
  
- chat, product, order, gateway, auth, frontend  
    - Deployment 및 Config yml 파일  
- monitoring  
    - Prometheus & Grafana  
- network  
    - certificate  
        - HTTPS 설정   
    - cluster-ip  
        - Cluster IP 설정  
    - ingress    
        - Ingress 설정  
    - control-center  
        - Confluent Kafka Control Center Load Balancer  
    - health-check  
        - health-check for Cluster IP  

## 네트워크 동작 방식  
   
```hcl
[Inbound]
Ingress -------------> Cluster IP -------------> Deployment  
[Deep Dive]
Ingress -------------> [Gateway Cluster IP] -----------> [Gateway Deployment] ----
  --------------------> [Other Cluster IPs] ------------------> [Other Deployments]
[Outbound]
NAT <-------------------------- Deployment
```