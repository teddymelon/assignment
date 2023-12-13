## 如何通過YAML創建對外Nginx服務
### 主要思路
- 透過YAML編寫 ``` Deployment ```、``` Service ```、``` Ingress ```來開放對外的服務。

### 檔案說明
說明本次YAML完成的事項，以及簡易說明。

+ ``` Deployment ```：處理Pod的創建與維護，容器Image從公開的ECR取得。
    + ``` name ```：```deployment-hello-sre```
    + ``` namespace ```：```hello-sre```
    + ``` image ```：```public.ecr.aws/c7v7e0l7/teddy:latest```

+ ``` Service ```：處理Deployment的網路流量處理。
    + ``` name ```：```service-hello-sre```
    + ``` namespace ```：```hello-sre```
    + ``` selector ```：```app.kubernetes.io/name: hello-sre```
    + ``` type ```：``` NodePort ```

+ ``` Ingress ```：處理Service，並且建置ALB。
    + ``` name ```：```ingress-hello-sre```
    + ``` namespace ```：```hello-sre```
    + ``` annotations ```：``` alb.ingress.kubernetes.io/scheme: internet-facing ```
    + ``` annotations ```：``` alb.ingress.kubernetes.io/target-type: ip ```
    + ``` ingressClassName ```：``` alb ```

### 參考連結
以下是本次實作的參考連結：

透過AWS的範本進行改寫

1.　https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
