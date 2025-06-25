# 멍탐정 AI (Meongtamjeong AI) 🕵️‍♂️

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Last Commit](https://img.shields.io/github/last-commit/meongtamjeongai/meongtamjeongai)
![License](https://img.shields.io/badge/license-MIT-blue)

**Terraform, FastAPI, Streamlit을 활용한 AI 기반 피싱 대응 훈련 플랫폼**

'멍탐정 AI'는 사용자가 AI 챗봇과의 대화를 통해 현실과 유사한 피싱 시나리오를 경험하고, 이에 대한 대응 능력을 안전하게 훈련할 수 있도록 설계된 서비스입니다. 이 프로젝트는 현대적인 DevOps 파이프라인과 효율적인 백엔드/프론트엔드 기술 스택을 기반으로 구축되었습니다.

---

## 🚀 Live Demo

| 서비스                | 링크                                                                                             | 설명                                     |
| -------------------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------- |
| 🖥️ **관리자 페이지**    | [admin.meong.shop](https://admin.meong.shop)                                                     | 사용자, 페르소나, 대화방 관리 및 테스트      |
| 📄 **API 문서**        | [meong.shop/scalar](https://meong.shop/scalar)                                                   | FastAPI로 자동 생성된 인터랙티브 API 문서 |
| ☁️ **Terraform Cloud** | [Workspace](https://app.terraform.io/app/meongtamjeongai/workspaces/meongtamjeongai-devops) | 인프라 상태 및 배포 관리                 |

---

## ✨ 주요 특징 (Key Features)

-   **🤖 AI 기반 피싱 시뮬레이션:** Google Gemini AI를 활용하여 다양한 피싱 시나리오를 생성하고, 사용자와의 대화를 통해 훈련을 진행합니다.
-   **🛡️ 안전한 파일 업로드:** AWS S3 Presigned URL을 사용하여 서버 부하 없이 안전하게 이미지를 업로드합니다.
-   **🔑 다양한 소셜 로그인:** Firebase, Kakao, Naver 등 익숙한 소셜 계정을 통해 간편하게 로그인할 수 있습니다.
-   **🏗️ 코드형 인프라 (IaC):** Terraform을 사용하여 모든 AWS 인프라(VPC, EC2, RDS 등)를 코드로 정의하고 관리합니다.
-   **🔄 자동화된 CI/CD:** GitHub Actions와 Terraform Cloud를 연동하여, 코드 Push 시 자동으로 테스트, 빌드, 배포가 이루어집니다.
-   **🐍 Python-Only 관리자 페이지:** 복잡한 프론트엔드 기술 없이, Streamlit만으로 데이터 관리 및 AI 기능 테스트 페이지를 신속하게 구축했습니다.

---

## 🗺️ 전체 아키텍처

이 프로젝트는 개발, 배포, 운영의 전 과정을 자동화하고, 각 구성 요소를 명확하게 분리하여 안정성과 확장성을 확보하는 것을 목표로 설계되었습니다.

![전체 아키텍처 다이어그램](assets/slide3-1.png)

---

## 🧰 기술 스택 (Tech Stack)

| 구분                        | 기술                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **⚙️ Backend**              | `FastAPI`, `Python`, `SQLAlchemy`, `Alembic`, `Gunicorn`                                                       |
| **🖥️ Frontend (Admin)**     | `Streamlit`, `Python`                                                                                        |
| **🧠 Database & AI**        | `PostgreSQL` (on AWS RDS), `Google Gemini API`                                                               |
| **☁️ Infrastructure**       | `AWS` (EC2, S3, ALB, VPC, RDS), `Terraform`, `Cloudflare` (DNS, Access)                                        |
| **🚀 DevOps & CI/CD**       | `Docker`, `Docker Compose`, `GitHub Actions`                                                                 |
| **🔐 Authentication**       | `JWT`, `Firebase Authentication`, `OAuth2` (Kakao, Naver)                                                      |
| **💻 Development Env**      | `Dev Container` (VS Code)                                                                                    |

---

## 📂 프로젝트 구조

<details>
<summary><strong>⚙️ 백엔드 (FastAPI) 폴더 구조 보기</strong></summary>

```
meongtamjeongai-backend/
├── alembic/              # 데이터베이스 마이그레이션
├── app/
│   ├── api/              # API 엔드포인트 및 의존성
│   ├── core/             # 핵심 설정, 보안
│   ├── crud/             # 데이터베이스 CRUD 함수
│   ├── db/               # 데이터베이스 세션 관리
│   ├── models/           # SQLAlchemy DB 모델
│   ├── schemas/          # Pydantic 데이터 스키마
│   └── services/         # 비즈니스 로직
├── scripts/              # DB 초기화, entrypoint 스크립트
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

</details>

<details>
<summary><strong>🖥️ 관리자 페이지 (Streamlit) 폴더 구조 보기</strong></summary>

```
meongtamjeongai-admin/
├── admin_app.py          # 메인 실행 파일, 페이지 분기
├── api/                  # 백엔드 API 호출 클라이언트
├── views/                # 각 페이지 UI 렌더링
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

</details>

<details>
<summary><strong>☁️ 인프라 (Terraform) 폴더 구조 보기</strong></summary>

```
terraform-aws-fastapi-infra/
├── modules/              # 재사용 가능한 인프라 단위 (VPC, EC2, RDS 등)
│   ├── acm/
│   ├── alb/
│   ├── ec2_backend/
│   └── ...
├── main.tf               # 전체 인프라 조립 (Root Module)
├── variables.tf          # 변수 정의
└── outputs.tf            # 출력값 정의
```

</details>

---

## 🛠️ 로컬 개발 환경 설정 (Getting Started)

이 프로젝트는 Docker와 Dev Container를 사용하여 간편하게 개발 환경 설정을 완료할 수 있습니다.

**사전 요구사항:**
-   [Git](https://git-scm.com/)
-   [Docker](https://www.docker.com/products/docker-desktop/)
-   [VS Code](https://code.visualstudio.com/)
-   [Dev Containers 확장 프로그램](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

**설정 단계:**

1.  **저장소 클론:**
    ```bash
    git clone https://github.com/your-github-username/meongtamjeong-ai.git
    cd meongtamjeong-ai
    ```

2.  **환경 변수 파일 생성:**
    -   `meongtamjeongai-backend/.env.dev.example` 파일을 복사하여 `.env.dev` 파일을 생성하고, 내용을 채웁니다.
    -   `meongtamjeongai-admin/.env.example` 파일을 복사하여 `.env` 파일을 생성하고, 내용을 채웁니다.

3.  **공용 Docker 네트워크 생성:**
    ```bash
    docker network create meong
    ```

4.  **Dev Container 실행:**
    -   VS Code에서 `meongtamjeongai-backend` 폴더를 엽니다.
    -   `Ctrl + Shift + P`를 눌러 명령 팔레트를 열고, `Dev Containers: Reopen in Container`를 선택합니다.
    -   (최초 실행 시 Dev Container 빌드에 몇 분 정도 소요될 수 있습니다.)

5.  **데이터베이스 마이그레이션:**
    -   새 터미널을 열고 아래 명령어를 실행하여 DB 스키마를 최신 상태로 업데이트합니다.
    ```bash
    alembic upgrade head
    ```

7.  **접속 확인:**
    -   **백엔드 API 문서:** [http://localhost:8000/scalar](http://localhost:8000/scalar)
    -   **관리자 페이지:** [http://localhost:8501](http://localhost:8501)

---

## 🧭 향후 계획 (Roadmap)

-   [ ] **테스트 코드 도입:** 단위/통합 테스트를 도입하여 시스템 안정성 확보
-   [ ] **아키텍처 개선:** 장기적 확장성을 위해 '도메인 중심 구조'로 점진적 리팩토링
-   [ ] **AI 경험 고도화:** 스트리밍 응답을 적용하여 실시간 채팅 경험 제공
-   [ ] **모니터링 및 캐싱:** 실시간 에러 로깅 및 캐싱 전략을 도입하여 성능 및 안정성 개선

---

## 📜 라이선스 (License)

이 프로젝트는 [MIT License](LICENSE)를 따릅니다.