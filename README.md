# Highly Available Kubernetes Cluster Setup

Bu proje, yüksek erişilebilirlik (HA) özelliklerine sahip bir Kubernetes cluster'ı oluşturmak için gerekli yapılandırmaları içerir. Vagrant kullanılarak otomatize edilmiş bir şekilde sanal makineler oluşturulur ve KubeSphere ile entegre bir Kubernetes ortamı kurulur.

![HA Kubernetes Cluster Architecture](https://kubesphere.io/images/docs/v3.x/installing-on-linux/high-availability-configurations/set-up-ha-cluster-using-keepalived-haproxy/architecture-ha-k8s-cluster.png)


## Mimari

Proje aşağıdaki bileşenlerden oluşmaktadır:

- **3 Master Node**: Kubernetes control plane bileşenlerini çalıştırır
- **2 Worker Node**: Uygulama workload'larını çalıştırır
- **2 Load Balancer Node**: HAProxy ve Keepalived ile yük dengeleme sağlar

## Ön Gereksinimler

- VirtualBox veya Libvirt
- Vagrant
- En az 16GB RAM
- En az 12 çekirdekli CPU

## Kurulum

1. Repo'yu klonlayın:
    ```bash
    git clone <repo-url>
    cd ha
    ```

2. Vagrant ile sanal makineleri başlatın:
    ```bash
    vagrant up
    ```

3. Load Balancer kurulumu:
   - Örnek HAProxy yapılandırması için `haproxy/haproxy.cfg` dosyasını kullanın.
   - Örnek Keepalived yapılandırması için `keepalived/keepalived.conf` dosyasını kullanın.

4. KubeSphere kurulumu:
   - Örnek yapılandırma dosyası: `kubesphere/config-sample.yaml`

## Node Bilgileri

### Master Nodes
- master1.example.com (192.168.56.101)
- master2.example.com (192.168.56.102)
- master3.example.com (192.168.56.103)

### Worker Nodes
- worker1.example.com (192.168.56.111)
- worker2.example.com (192.168.56.112)

### Load Balancer Nodes
- lb1.example.com (192.168.56.121)
- lb2.example.com (192.168.56.122)

## Notlar

- Tüm node'larda root şifresi: `admin`
- API Server endpoint: https://192.168.56.100:6443
- Node'lar arası iletişim için private network kullanılmaktadır.
- Ubuntu 20.04 LTS işletim sistemi kullanılmaktadır.
- Vagrant box versiyonu: 4.2.6
