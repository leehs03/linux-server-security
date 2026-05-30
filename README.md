# 🔐 리눅스 서버 접근통제 환경 구축

> SGA솔루션즈 TTS사업본부 지원 포트폴리오 | 컴퓨터정보학부

## 📋 프로젝트 개요

VirtualBox 기반 Ubuntu 22.04 LTS 서버 환경에서 실무 수준의 접근통제 보안 설정을 직접 구축하고 검증한 프로젝트입니다.

## 🛠️ 사용 기술

| 기술/도구 | 버전 | 용도 |
|----------|------|------|
| VirtualBox | 7.x | 가상 서버 환경 구축 |
| Ubuntu Server | 22.04.5 LTS | 리눅스 서버 운영체제 |
| OpenSSH | 8.9 | SSH 원격 접속 및 보안 설정 |
| UFW | 0.36 | 방화벽 정책 관리 |
| MobaXterm | 26.3 | SSH 클라이언트 터미널 |

## ✅ 구현 내용

- **SSH 원격 접속 설정** - 포트 포워딩(2222→22) 기반 MobaXterm SSH 접속
- **root 계정 원격 접속 차단** - PermitRootLogin no 설정
- **방화벽(UFW) 설정** - 기본 차단 + SSH 포트만 허용
- **계정 권한 분리** - 최소 권한 원칙 적용 (관리자/일반 계정 분리)
- **SSH 키 인증 설정** - RSA 4096비트 키 기반 인증

## 📁 파일 구성

linux-server-security/
├── README.md
├── docs/
│   └── SGA_포트폴리오_기술문서.pdf
└── screenshots/
├── 01_방화벽_상태확인.png
├── 02_root차단_확인.png
├── 03_계정권한_분리.png
├── 04_SSH키_인증확인.png
└── 05_SSH서비스_상태.png

## 🔑 핵심 보안 설정

### root 로그인 차단
```bash
# /etc/ssh/sshd_config
PermitRootLogin no
```

### 방화벽 설정
```bash
sudo ufw enable
sudo ufw allow ssh
sudo ufw default deny incoming
```

### SSH 키 인증
```bash
ssh-keygen -t rsa -b 4096
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

## 📊 보안 설정 결과

| 보안 설정 항목 | 설정 내용 | 결과 |
|--------------|----------|------|
| SSH 원격 접속 | 포트 포워딩 2222→22 | ✅ 정상 접속 |
| root 접속 차단 | PermitRootLogin no | ✅ 차단 확인 |
| 방화벽 활성화 | UFW + SSH 허용 | ✅ Active |
| 계정 권한 분리 | sudo 그룹 분리 | ✅ 확인 |
| SSH 키 인증 | RSA 4096비트 | ✅ 설정 완료 |
