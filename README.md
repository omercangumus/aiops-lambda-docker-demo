<div align="center">

# 🚀 AWS Lambda Docker Pipeline  
**Container Image → ECR → Lambda Deployment**

Cloud • Serverless • Docker • AIOps • CI/CD

---

![AWS](https://img.shields.io/badge/AWS-Lambda-orange?logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Container-blue?logo=docker&logoColor=white)
![ECR](https://img.shields.io/badge/AWS-ECR-red?logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.9-yellow?logo=python)
![Status](https://img.shields.io/badge/Project-Active-brightgreen)

</div>

---

## 📌 Proje Açıklaması

Bu proje, **Docker ile paketlenmiş bir AWS Lambda fonksiyonunun**  
**AWS ECR’e pushlanması** ve ardından **Lambda’nın container image ile güncellenmesi** için oluşturulmuş modern bir örnektir.

AIOps ve Cloud öğrenme sürecimde:

- Container tabanlı Lambda geliştirme  
- ECR workflow yönetimi  
- AWS CLI ile otomasyon  
- Pipeline mantığını kavrama  
- İleride Terraform ile tamamen otomatik altyapı kurma  

gibi konuları pratik etmek için geliştirilmiştir.

---

## 📁 Proje Yapısı

project-folder/
│
├── Dockerfile # Lambda için Docker image
├── app.py # Python Lambda fonksiyonu
├── requirements.txt # Pip bağımlılıkları
└── README.md

yaml
Kodu kopyala

---

## 🧠 Lambda Fonksiyonu (Basit Örnek)

```python
def handler(event, context):
    return "Merhaba, ben Docker içinden çalışan Lambda fonksiyonuyum!"
Bu fonksiyon Docker image içine gömülür → ECR’e pushlanır → Lambda container olarak çalıştırır.

🛠 Gereksinimler
Teknoloji	Amaç
Docker	Lambda’nın container olarak paketlenmesi
AWS CLI	ECR & Lambda yönetimi
IAM	ECR push + Lambda update izinleri
(İsteğe bağlı) CI/CD	Otomatik build → push → deploy

🐳 Docker Image Oluşturma
bash
Kodu kopyala
docker build -t lambda-docker-demo .
🔐 ECR Login
bash
Kodu kopyala
aws ecr get-login-password --region eu-west-1 \
| docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com
🏷️ Image Tag Verme
bash
Kodu kopyala
docker tag lambda-docker-demo:latest <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
📦 Image Pushlama
bash
Kodu kopyala
docker push <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
⚡ Lambda Güncelleme
Yeni image pushlandıktan sonra Lambda’nın kodunu güncelle:

bash
Kodu kopyala
aws lambda update-function-code \
  --function-name lambda-docker-demo \
  --image-uri <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
🔄 CI/CD Pipeline (Örnek Akış)
Kod push → GitHub/GitLab pipeline tetiklenir

Docker image build edilir

ECR’e pushlanır

Lambda otomatik olarak güncellenir

CloudWatch log’ları ile doğrulama yapılır

Pipeline dosyasını daha sonra ekleyeceğim.

🌍 Yol Haritası
Durum	Yapılacak
✅	Docker + Lambda entegrasyonu
✅	ECR push & Lambda update
🔜	GitHub Actions pipeline
🔜	Terraform ile tam otomatik altyapı (/terraform klasörü)
🔜	CloudWatch + Alarm + AIOps gözlemlenebilirlik ekleme

👤 Geliştirici
Ömer Can Gümüş
AIOps • Cloud • DevOps • Serverless

