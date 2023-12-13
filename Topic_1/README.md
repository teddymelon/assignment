## 如何通過Terraform創建AWS EKS Cluster
### 主要思路
- terraform上通過Module來進行EKS的創建，並且需先滿足前置VPC Network等等的建立。
- 由於後續需要部署ALB，因此也需要創建alb-ingress-controller，但需要先完成LB-Role、Service Account的創建。

### 檔案說明
說明本次Terraform檔案各自完成的事項，以及Config的簡易說明。

+ ``` main.tf ```：處理VPC、EKS的創建
    + ``` provider "aws" ```：服務提供者
    + ``` locals ```：包含多個變數
    + ``` module "vpc" ```：處理vpc的建置
    + ``` module "eks" ```：真正創建eks的部分
    + ``` resource "aws_security_group_rule" "http_allow" ```：處理安全組的設定，多添加一條允許http進入node

+ ``` serviced-account.tf ```：處理alb、K8S Service Account
    + ``` module "lb_role" ```：創立Load-Balancer的IAM權限
    + ``` resource "kubernetes_service_account" "service-account" ```：創建Service Account用來操作ALB

+ ``` helm.tf ```：處理helm、alb-ingress-controller
    + ``` provider "kubernetes" ```：服務提供者
    + ``` provider "helm" ```：服務提供者
    + ``` resource "helm_release" "alb-controller" ```：創建alb-controller

+ ``` output.tf ```：處理丟出來的值，但這次沒有特別使用到。

### 採坑處

1. 測試完畢的ALB，要用指令刪除 kubectl delete -f ，不然terraform沒辦法處理。

2. 第一次建置完成後，發現服務產生504 time out，後來發現是module中的安全組沒有調整允許80(ALB無法回後端值區拿資料)，因此才在　``` Main.tf ```　中添加Security Group的設定。


### 參考連結
以下是本次實作的參考連結：

1.　https://andrewtarry.com/posts/terraform-eks-alb-setup

2.　https://www.youtube.com/watch?v=ZfjpWOC5eoE&ab_channel=AntonPutra

3.　https://andrewtarry.com/posts/terraform-eks-alb-setup/

4.　https://medium.com/@StephenKanyiW/provision-eks-with-terraform-helm-and-a-load-balancer-controller-821dacb35066

5.　https://github.com/terraform-aws-modules/terraform-aws-eks/blob/master/examples/eks_managed_node_group/main.tf

6.　https://github.com/ascode-com/wiki/blob/main/terraform-eks/complete-example.tf

7.　https://registry.terraform.io/modules/terraform-aws-modules/eks/aws/latest 

8.　https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule