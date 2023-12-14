## 如何通過Github Action的CICD流程，在EKS上創建對外服務
### 主要思路
- 通過撰寫cicd.yml來進行CICD的自動化部署

### 前情提要
- 準備好一份Dockerfile  （欲部署的Docker Image）
- 準備好一份hello-sre.yaml  （欲部署在EKS上的yaml）
- 準備好一座EKS Cluster （通過Topic-1的Terraform創建）

### 檔案說明
[Github Action 簡介](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)

Github Action的Config File存放在``` .github/workflows ```下的``` cicd.yml ```。

以下將會說明CICD的流程：

(``` cicd.yml ``` 中也有相對應的說明，)


+ ``` 在Action Server中安裝kubectl ```

+ ``` 在Action Server中設置AWS的Credential ```

+ ``` 在Action Server中登入ECR私有庫 or 公有庫 (可通過不同參數對應私有或者公有) ```

+ ``` 將Dockerfile打包成Image ```

+ ``` 推送Image到相對應的庫中 ```

+ ``` 更新kube-config，確保Action Server可以登入到EKS Control Panel中 ```

+ ``` 通過kubectl apply，部署hello-sre.yaml到EKS中 ```

*注意事項：Github Action各個action也有版本限制，類似terraform的Module，務必要定期更新，參考連結會放上本次參考到並且調整到的action Github連結。

### 參考連結
以下是本次實作的參考連結：

1.　https://github.com/devopshint/deploy-nodejs-app-to-EKS-using-GitHub-Actions/tree/main

2.　https://github.com/aws-actions/amazon-ecr-login
 
3. https://github.com/Azure/setup-kubectl

4. https://github.com/aws-actions/configure-aws-credentials