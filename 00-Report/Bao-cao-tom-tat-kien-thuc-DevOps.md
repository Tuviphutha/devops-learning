# BÁO CÁO TÓM TẮT KIẾN THỨC VỀ DEVOPS

> Tổng hợp kiến thức nền tảng, kiến trúc hệ thống và định hướng phát triển.

---

# 1. DevOps là gì?

DevOps là thuật ngữ kết hợp giữa **Development (Phát triển phần mềm)** và **Operations (Vận hành hệ thống)**.

DevOps không đơn thuần là một vị trí công việc hay một bộ công cụ cụ thể, mà là sự tổng hòa của các yếu tố cốt lõi:

> **DevOps = Văn hóa làm việc + Quy trình chuẩn hóa + Tự động hóa + Bộ công cụ + Tư duy cải tiến liên tục**

## Mục tiêu chính

- Rút ngắn thời gian đưa phần mềm từ mã nguồn (**Source Code**) đến môi trường thực tế (**Production**).
- Nâng cao tính ổn định, độ tin cậy, khả năng quan sát (**Observability**) và khả năng tự phục hồi của toàn hệ thống.

---

# 2. Vai trò và Giá trị của DevOps

Trong mô hình truyền thống, **Developer** và **Operations** thường làm việc tách biệt, tạo nên bức tường ngăn cách được gọi là **Wall of Confusion**.

Developer tập trung viết code và bàn giao tính năng mới thật nhanh, trong khi Operations chịu trách nhiệm giữ cho máy chủ ổn định và hạn chế thay đổi.

Sự khác biệt giữa các môi trường có thể dẫn đến:

- Lỗi phát sinh.
- Chậm trễ bàn giao.
- Khó quy trách nhiệm.

DevOps giải quyết bài toán này thông qua 3 trụ cột cốt lõi:

## 2.1. Chuẩn hóa môi trường

Đảm bảo ứng dụng chạy đồng nhất từ máy tính cá nhân (**Local**) đến môi trường **Staging** và **Production**.

## 2.2. Tự động hóa luồng chuyển giao

Giảm thiểu tối đa các thao tác thủ công vốn tiềm ẩn nhiều sai sót do con người.

## 2.3. Vòng phản hồi liên tục

Dữ liệu vận hành thực tế được chuyển ngược về đội ngũ phát triển để liên tục cải tiến chất lượng phần mềm.

---

# 3. Vòng đời DevOps (DevOps Lifecycle)

Vòng đời DevOps là một chu trình liên tục khép kín dạng vô cực (**Infinite Loop**):

```text
PLAN
  ↓
CODE
  ↓
BUILD
  ↓
TEST
  ↓
RELEASE
  ↓
DEPLOY
  ↓
OPERATE
  ↓
MONITOR
  ↓
FEEDBACK
  ↓
PLAN
```

Hoặc:

```text
PLAN → CODE → BUILD → TEST → RELEASE → DEPLOY → OPERATE → MONITOR → FEEDBACK → PLAN
```

## Điểm mấu chốt

Đây là chu trình không ngừng nghỉ.

Dữ liệu giám sát và phản hồi từ bước **Operate** và **Monitor** được sử dụng làm căn cứ lập kế hoạch (**Plan**) cho các chu kỳ phát triển tiếp theo.

---

# 4. Các Trụ Cột Kiến Thức Nền Tảng

## 4.1. CI/CD

**CI/CD** là viết tắt của:

- **Continuous Integration** – Tích hợp liên tục.
- **Continuous Delivery** – Chuyển giao liên tục.
- **Continuous Deployment** – Triển khai liên tục.

### CI – Continuous Integration

CI tự động hóa quá trình:

- Tích hợp mã nguồn.
- Build ứng dụng.
- Chạy bộ kiểm thử.

Các loại kiểm thử phổ biến:

- Unit Test.
- Integration Test.

Quá trình này thường được kích hoạt ngay khi lập trình viên đẩy một commit mới lên Git.

### CD – Continuous Delivery / Deployment

#### Continuous Delivery

Đảm bảo mã nguồn luôn ở trạng thái sẵn sàng phát hành lên **Production** sau bước phê duyệt.

#### Continuous Deployment

Tự động triển khai trực tiếp ứng dụng lên **Production** mà không cần phê duyệt thủ công.

### Luồng Pipeline tiêu chuẩn

```text
Developer Push Code
        ↓
Build & Compile
        ↓
Automated Test
        ↓
Security Scan
        ↓
Build Container Image
        ↓
Push to Registry
        ↓
Deploy to Cluster
```

---

## 4.2. Docker và Công nghệ Container

Container là giải pháp đóng gói toàn bộ:

- Mã nguồn ứng dụng.
- Dependencies.
- Thư viện liên kết.
- Cấu hình.

Tất cả được đóng gói thành một đơn vị độc lập.

Container giúp giải quyết vấn đề kinh điển:

> "Chạy được trên máy của tôi nhưng lại lỗi trên server."

### Docker Image

Docker Image là một khuôn mẫu tĩnh (**Template**) chỉ đọc, chứa:

- Mã nguồn.
- Môi trường thực thi.
- Cấu hình cần thiết.

Docker Image được sử dụng để khởi tạo Container.

### Docker Container

Docker Container là một thực thể (**Instance**) đang thực thi được khởi tạo từ Docker Image.

Mô hình đơn giản:

```text
Docker Image
      ↓
docker run
      ↓
Docker Container
```

---

## 4.3. Container Runtime và Kiến trúc cấp thấp

Container Runtime là thành phần cấp thấp chịu trách nhiệm:

- Quản lý vòng đời Container.
- Tạo Container.
- Chạy Container trực tiếp trên Linux Kernel.

### Mô hình phân tầng Runtime

```text
Docker Engine / Kubernetes
            ↓
containerd
(High-level Runtime)
            ↓
runc
(Low-level Runtime / OCI)
            ↓
Linux Kernel
(Namespaces & Cgroups)
```

Kubernetes kết nối linh hoạt với các Container Runtime thông qua chuẩn giao diện:

```text
CRI
(Container Runtime Interface)
```

---

## 4.4. Điều phối Container với Kubernetes (K8s)

Kubernetes là nền tảng điều phối Container (**Container Orchestration**) giúp quản lý số lượng lớn Container trên cụm máy chủ phân tán.

### Các khả năng cốt lõi

- Tự động triển khai và thu hồi (**Rollout / Rollback**).
- Tự động co giãn (**Auto Scaling**).
- Tự phục hồi khi xảy ra lỗi (**Self-healing**).
- Cân bằng tải (**Load Balancing**).
- Khám phá dịch vụ (**Service Discovery**).

### Các đối tượng quan trọng trong Kubernetes

- Pod
- Deployment
- Service
- Ingress
- ConfigMap
- Secret
- Namespace
- StatefulSet

---

## 4.5. Cơ sở hạ tầng dưới dạng mã (Infrastructure as Code – IaC)

**Infrastructure as Code (IaC)** là phương pháp thiết lập, quản lý và cung cấp tài nguyên hạ tầng thông qua mã nguồn.

Mã nguồn có thể được quản lý phiên bản bằng:

```text
Git
```

IaC thay thế việc cấu hình thủ công trên giao diện máy chủ.

### Terraform

Terraform chuyên dùng để khởi tạo và phân bổ tài nguyên hạ tầng (**Infrastructure Provisioning**), ví dụ:

- VPC.
- Cloud VM.
- Subnet.
- Firewall.
- Managed Database.

### Ansible

Ansible chuyên dùng để:

- Quản trị cấu hình (**Configuration Management**).
- Cài đặt phần mềm.
- Tự động hóa các tác vụ quản trị hàng loạt trên Server.

---

## 4.6. Điện toán đám mây (Cloud Computing)

Môi trường thực thi của DevOps hiện đại gắn liền với các nền tảng đám mây lớn như:

- AWS.
- Google Cloud Platform (GCP).
- Microsoft Azure.

### Các thành phần quan trọng

- Virtual Machines.
- VPC & Networking.
- IAM & Phân quyền.
- Managed Database.
- Object Storage.
- Managed Kubernetes.

Ví dụ:

```text
AWS → EKS
GCP → GKE
Azure → AKS
```

---

# 5. Hệ thống Giám sát, Nhật ký và Cảnh báo

Sau khi ứng dụng được triển khai lên môi trường **Production**, hệ thống bắt buộc phải được theo dõi liên tục nhằm:

- Phát hiện sớm các bất thường.
- Theo dõi tình trạng hệ thống.
- Tối ưu hiệu năng.
- Hỗ trợ điều tra sự cố.

| Phân hệ | Mục tiêu & Chỉ số theo dõi | Công cụ phổ biến |
|---|---|---|
| Monitoring & Metrics | CPU, RAM, Disk, Network I/O, Response Time, Error Rate | Prometheus, Datadog, Zabbix |
| Visualization | Xây dựng Dashboard trực quan hóa các chỉ số theo thời gian thực | Grafana |
| Centralized Logging | Thu thập, phân tích và tra cứu log tập trung từ các Microservices để điều tra sự cố | ELK Stack, Loki |
| Alerting | Tự động gửi thông báo khi có lỗi nghiêm trọng hoặc chạm ngưỡng cảnh báo | Alertmanager, PagerDuty, Slack / Telegram Bot |

### ELK Stack

ELK Stack bao gồm:

- Elasticsearch.
- Logstash.
- Kibana.

---

# 6. Tổng quan công việc của DevOps Engineer

Một kỹ sư DevOps chuyên nghiệp chịu trách nhiệm trên các mảng công việc chính sau:

## 6.1. Quản trị hệ thống và mạng

- Quản trị Linux Server.
- Cấu hình mạng.
- DNS.
- Chứng chỉ SSL/TLS.
- Security Hardening.

## 6.2. Tự động hóa CI/CD

Thiết kế và tối ưu Pipeline tự động với các công cụ như:

- GitHub Actions.
- GitLab CI.
- Jenkins.

## 6.3. Đóng gói và điều phối

- Container hóa ứng dụng bằng Docker.
- Điều phối cụm Kubernetes (K8s) quy mô lớn.

## 6.4. Infrastructure as Code

- Viết mã khởi tạo hạ tầng Cloud bằng Terraform.
- Tự động cấu hình bằng Ansible.

## 6.5. Vận hành Cloud

Quản lý và tối ưu:

- Chi phí.
- Hiệu năng.
- Bảo mật.

Trên các nền tảng:

- AWS.
- GCP.
- Azure.

## 6.6. Giám sát và xử lý sự cố

- Thiết lập Prometheus.
- Xây dựng Dashboard bằng Grafana.
- Thu thập Log bằng ELK hoặc Loki.
- Tham gia quy trình trực ứng cứu sự cố (**Incident Response**).

## 6.7. Lập trình kịch bản

Viết Script để tự động hóa các tác vụ định kỳ bằng:

- Bash Shell.
- Python.

---

# 7. Mô Hình Kiến Trúc Luồng Vận Hành Thực Tế

Luồng chuyển giao mã nguồn từ lập trình viên đến môi trường vận hành thực tế:

## Bước 1: Developer Push Code

Developer thực hiện:

```text
Commit → Push
```

Mã nguồn được đẩy lên:

- GitHub Repository.
- GitLab Repository.

---

## Bước 2: CI/CD Pipeline được kích hoạt

Webhook kích hoạt CI/CD Pipeline tự động chạy:

- Unit Test.
- Linting.
- Security Scan.

Một số công cụ:

- SonarQube.
- Trivy.

---

## Bước 3: Build Docker Image

CI Pipeline đóng gói ứng dụng thành Docker Image.

Image được gắn thẻ phiên bản (**Semantic Tagging**).

Ví dụ:

```text
my-app:1.0.0
my-app:1.0.1
```

---

## Bước 4: Push Image lên Container Registry

Docker Image được đẩy lên Container Registry như:

- Harbor.
- AWS ECR.
- Docker Hub.

---

## Bước 5: CD Pipeline / GitOps triển khai ứng dụng

CD Pipeline hoặc GitOps Tool như:

```text
ArgoCD
```

đồng bộ và cập nhật các Manifest lên Kubernetes Cluster.

---

## Bước 6: Kubernetes triển khai ứng dụng

Kubernetes triển khai ứng dụng dưới dạng Pods.

Các chiến lược triển khai có thể bao gồm:

- Rolling Update.
- Blue-Green Deployment.

Mục tiêu là:

```text
Zero Downtime
```

---

## Bước 7: Monitoring và Alerting

Prometheus và Loki liên tục thu thập:

- Metrics.
- Logs.

Khi xảy ra sự cố, hệ thống có thể gửi cảnh báo qua:

- Slack.
- PagerDuty.

### Toàn bộ luồng

```text
Developer
    ↓
GitHub / GitLab
    ↓
CI Pipeline
    ↓
Test + Security Scan
    ↓
Build Docker Image
    ↓
Container Registry
    ↓
CD Pipeline / GitOps
    ↓
Kubernetes Cluster
    ↓
Application Pods
    ↓
Prometheus + Loki
    ↓
Alertmanager
    ↓
Slack / PagerDuty
```

---

# 8. Tổng Kết và Tư Duy Cốt Lõi

Sau quá trình tìm hiểu, em thấy DevOps không chỉ yêu cầu biết sử dụng một vài công cụ như Docker hoặc Kubernetes.

Một DevOps Engineer cần kiến thức nền tảng về:

- Linux.
- Network.
- Automation.
- Cloud.
- Vận hành hệ thống Production.

## Nguyên lý vận hành xuyên suốt

```text
Source Code
    ↓
Build
    ↓
Test
    ↓
Package
    ↓
Deploy
    ↓
Operate
    ↓
Monitor
    ↓
Continuous Improvement
```

DevOps là quá trình kết nối giữa phát triển phần mềm và vận hành hệ thống, hướng tới:

- Tự động hóa.
- Chuẩn hóa.
- Triển khai nhanh hơn.
- Hệ thống ổn định hơn.
- Phát hiện và xử lý sự cố nhanh hơn.
- Cải tiến liên tục dựa trên dữ liệu vận hành thực tế.

---

## Người thực hiện

**Đỗ Duy Tùng**
