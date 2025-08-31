# Witple Infrastructure

Witple 프로젝트를 위한 AWS 인프라스트럭처 코드입니다.

## 🏗️ **인프라 구성**

### **주요 구성요소:**
- **EKS 클러스터**: 쿠버네티스 오케스트레이션1
- **VPC & 네트워킹**: 프라이빗/퍼블릭 서브넷
- **ECR 저장소**: 도커 이미지 저장소
- **RDS 데이터베이스**: PostgreSQL 데이터베이스
- **GitHub Actions OIDC**: CI/CD 파이프라인 연동
- **Route 53 & ACM**: 도메인 및 SSL 인증서 관리

## 🚀 **시작하기**

### **1. 사전 요구사항**
- Terraform >= 1.0
- AWS CLI 설정
- GitHub 저장소

### **2. 설정**
```bash
# 저장소 클론
git clone https://github.com/KJ-31/witple_infrastructure.git
cd witple_infrastructure

# 설정 파일 복사
cp terraform.tfvars.example terraform.tfvars

# terraform.tfvars 파일 편집
# - GitHub 저장소 정보 업데이트
# - 도메인 설정 (선택사항)
```

### **3. 배포**
```bash
# Terraform 초기화
terraform init

# 배포 계획 확인
terraform plan

# 인프라 배포
terraform apply
```

## 📁 **파일 구조**

```
witple_infrastructure/
├── main.tf                    # 메인 인프라 구성
├── variables.tf               # 변수 정의
├── outputs.tf                 # 출력 값 정의
├── oidc-setup.tf             # GitHub Actions OIDC 설정
├── aws-load-balancer-controller-policy.json  # 로드밸런서 정책
├── terraform.tfvars.example   # 설정 예시 파일
├── .gitignore                 # Git 제외 파일
└── README.md                  # 프로젝트 설명
```

## 🔧 **주요 설정**

### **AWS 리전**
- 기본: `ap-northeast-2` (서울)

### **EKS 클러스터**
- 클러스터명: `witple-cluster`
- 버전: `1.31`
- 노드 타입: `t3.medium`

### **RDS 데이터베이스**
- 엔진: PostgreSQL 15.13
- 인스턴스 타입: `db.t3.micro`
- 데이터베이스명: `witple_db`

## 🔐 **보안**

- 모든 리소스에 적절한 태그 적용
- IAM 최소 권한 원칙 적용
- GitHub Actions OIDC 인증 사용
- 민감한 정보는 자동 생성 (terraform.tfvars에 하드코딩 금지)

## 📝 **태그 구조**

모든 리소스에 다음 태그가 적용됩니다:
- `Name`: 리소스별 고유 이름
- `Project`: "witple"
- `Environment`: "production"
- `ManagedBy`: "terraform"

## 🆘 **문제 해결**

### **일반적인 문제들:**
1. **S3 백엔드 접근 오류**: AWS 자격 증명 확인
2. **EKS 클러스터 생성 실패**: VPC 설정 확인
3. **GitHub Actions OIDC 오류**: 저장소 정보 확인

## 📞 **지원**

문제가 발생하면 GitHub Issues를 통해 문의해주세요.
