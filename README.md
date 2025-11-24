<div align="center">

<!-- logo -->
<img src="https://user-images.githubusercontent.com/80824750/208554611-f8277015-12e8-48d2-b2cc-d09d67f03c02.png" width="400"/>

### Project: 슬기로운 소비생활(Slgm)

<br/> [<img src="https://img.shields.io/badge/프로젝트 기간-2025.07.25~2025.08.24-green?style=flat&logo=&logoColor=white" />]()

</div> 

## 📝 소개
이 앱은 무조건 아끼는 절약이 아니라, '낭비를 줄이고 가치 있는, 실용성 있는 '현명한 선택'을 할 수 있게 도와주고자 합니다.

- 프로젝트 소개
- 프로젝트 화면 구성 또는 프로토 타입
- 프로젝트 API 설계
- 사용한 기술 스택
- 프로젝트 아키텍쳐
- 기술적 이슈와 해결 과정
- 프로젝트 팀원
- 트러블 슈팅



<br />


## 🗂️ APIs
작성한 API는 아래에서 확인할 수 있습니다.

👉🏻 [API 바로보기](https://band-collar-06a.notion.site/APIs-256cf133eeae80ae9e1cea382453b671?source=copy_link)


<br />

## ⚙ 기술 스택
### Back-end
<div>
<img src="https://img.icons8.com/?size=100&id=90519&format=png&color=000000" width="80">
<img src="https://img.icons8.com/?size=100&id=A3Ulk2RcONKs&format=png&color=000000" width="80">
<img src="https://img.icons8.com/?size=100&id=JRnxU7ZWP4mi&format=png&color=000000" width="80">
</div>

### Infra
<div>
<img src="https://img.icons8.com/?size=100&id=e6uRfPIDgoXi&format=png&color=000000" width="80">
</div>

### Tools
<div>
<img src="https://img.icons8.com/?size=100&id=3tC9EQumUAuq&format=png&color=000000" width="80">
<img src="https://img.icons8.com/?size=100&id=nvtEH6DpqruC&format=png&color=000000" width="80">
</div>

<br />


<br />

## 🤔 기술적 이슈와 해결 과정
- Over-Fetch 와 Under-Fetch 개념 및 대안
  - [오버 페치(Over-Fetch)와 언더 페치(Under-Fetch)란?](https://happydhkim.tistory.com/entry/%EC%98%A4%EB%B2%84-%ED%8E%98%EC%B9%98Over-Fetch%EC%99%80-%EC%96%B8%EB%8D%94-%ED%8E%98%EC%B9%98Under-Fetch%EB%9E%80)
- 순환참조 해결을 위한 CQRS 패턴
  - [Spring CQRS 패턴](https://rebugs.tistory.com/895)
- 글로벌 예외 처리
  - [Spring Java 예외(Exception) 처리 전략](https://turtledev.tistory.com/67)
- 트랜잭션에서 외부 API 호출(ai) 
  - [트랜잭션 내에서 외부 API 호출을 하겠다고요?!!! ](https://engineerinsight.tistory.com/412)
- Service 코드 역할 분배
  - [SAGA 패턴이란?](https://azderica.github.io/01-architecture-msa/)

<br />

## 👥 백엔드 팀원
|Backend|Backend|Backend|
|:---:|:---:|:---:|
| ![](https://github.com/holychann.png?size=120) | ![](https://github.com/todaysunny612.png?size=120) | ![](https://github.com/higakaga.png?size=120)|
|[조성찬](https://github.com/holychann)|[최희선](https://github.com/todaysunny612)|[이동호](https://github.com/higakaga)

<br />

| 이름 | 담당 |
|------|------|
| 조성찬 | 유저, 결제내역, 포인트, 캐릭터, 아이템, 카테고리, 솔루션, 알림 도메인 <br />CI/CD 파이프라인 / 인프라 관리 (AWS S3, ECR, App Runner) / API, ERD 설계 |
| 최희선 | 유저, 제휴, 기프티콘 도메인 / API, ERD 설계 |
| 이동호 | 챌린지 도메인 / API, ERD 설계 |

<br />

### ✍️ My Contribution 
<br />
<br />
  

> \[!NOTE]
> 아래 항목들은 “담당 파트/스택” 섹션을 **반복하지 않고**, 제가 **직접 주도/기여**한 내용과 **문제 해결 중심**으로 정리했습니다.

<br />

---
## 문제점과 해결

<br />

* **외부 API Transactional 적용**  
  Transactional 을 제대로 알기 전에 전체 클래스에 Transactional 을 적용하여 AI 사용 시 장시간(약 10초) 커넥션을 점유하는 문제가 있었습니다.  
  외부 API 를 제외하고 DB 에 쓰기 작업을 하는 부분만 Transactional 을 적용하여 문제를 해결하였습니다.  
  <span style="color: grey">자세한 내용 정리</span>: [트랜잭션 내에서 외부 API 호출 시 문제점](https://velog.io/@east0323/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EB%82%B4%EC%97%90%EC%84%9C-%EC%99%B8%EB%B6%80-API-%ED%98%B8%EC%B6%9C-%EC%8B%9C-%EB%AC%B8%EC%A0%9C%EC%A0%90)

* **순환 참조 이슈**  
  CQRS 패턴을 도입하여 서비스 역할을 `Command` 와 `Query` 로 분리하여 순환 참조를 해결하였습니다.

* **의사결정&트레이드오프 → 최적화 vs 편리함**
한 화면에서 최대 7개의 도메인의 API 를 호출이 필요하여, 최적화를 위해 Facade 패턴을 제안했지만  
해커톤 맥락(낮은 트래픽, 짧은 기간)을 고려해 **도메인별 개별 API 호출** 방식을 채택하였습니다.(일부 화면에서 최대 7회 호출)
  
* **AWS 과금 이슈**  
  AWS 를 처음 사용하는 상황에서 VPC 등으로 private 한 환경을 구축했으나, 예상하지 못한 과금으로 대안을 찾던 중 public 의 존재 확인 후 변경하였습니다.
  이로 인해서 배포 비용 절감, 배포 유지기간 증가와 같은 효과를 보았습니다.


<br />

---

## 협업&리더쉽

* **API 명세 주도**: 엔드포인트/페이로드/에러 케이스 주도하여 관리하였습니다.
* **코드 리뷰 & 컨벤션 정립**: 브랜치 전략, 커밋 메시지 규칙, 패키지 구조/네이밍 가이드 등을 정리하여 팀원과 공유하였습니다.
* **문서화**: README/ERD 등을 직접 관리하고 변경사항이 생기는 즉시 적용 및 공유하였습니다.

<br />

---

<br />

