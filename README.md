## Assignment Work
### 主要問題
1. 如何通過 ``` Terraform ``` 來創建K8S環境
2. 如何使用 ``` Dockerfile ``` 打包 ``` Specified Nginx Docker Image ```
3. 如何撰寫 ``` Yaml File ``` 來創建 ``` 問題2 ```的 ``` Docker Image ```，並且通過``` AWS ALB ```讓``` 外部使用者 ```存取。
4. 如何通過 ``` CICD Tool ``` 來自動化 ``` 問題2、3 ```

**備註：CICD的部分模擬的是線上已經有Test/Production Environment，若需要自動化Terraform創建，僅需在CICD中加入Terraform的自動化部署。

### 選擇環境
本次Assignment使用以下環境與工具進行實作：
+ ``` AWS EKS ```
+ ``` AWS ECR ```
+ ``` Docker ```
+ ``` K8S Manifest - YAML ```
+ ``` Github Action ```


### 檔案對應


1. ``` Topic_1 ```對應``` 問題1 ```

2. ``` Topic_2 ```對應``` 問題2 ```

3. ``` Topic_3 ```對應``` 問題3 ```

4. ``` Topic_4 ```對應``` 問題4 ```


### 注意事項
本次Assignment是循序漸進的完成，從 ``` 問題2 ``` > ``` 問題1 ``` > ``` 問題3 ``` > ``` 問題4 ```，並且過程中須注意以下幾點：

+ 撰寫Terraform時，``` AWS EKS ```需同時撰寫``` Helm ```相關Config來安裝``` LB-Ingress-Controller ```，並且須設定好相關的``` LB-Role ``` & ``` Service Account ```。

+ 撰寫``` YAML ```時，需注意``` ALB Ingress ```的撰寫方式。

