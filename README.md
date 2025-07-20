# 🎤 팬덤 순위 예측 데이터베이스 프로젝트

> **음악방송 1위 점수 예측을 위한 팬덤 중심 데이터베이스 설계 및 구현 프로젝트**

---

## 📌 프로젝트 개요

K-POP 팬덤은 아티스트의 음악방송 1위를 위해 다양한 지표들을 실시간으로 분석하고 전략을 수립합니다. 본 프로젝트는 팬덤 전용 플랫폼을 위한 데이터베이스를 설계하여, 스트리밍 수, 유튜브 조회수, 음반 판매량, 앱 투표수 등 주요 성적 데이터를 종합·분석할 수 있는 기반을 제공합니다.

특히 본 데이터베이스는 **인증된 회원만 접근 가능한 팬사이트**를 전제로, 팬들이 실시간 데이터를 공유하고 투표 전략을 수립할 수 있도록 설계되었습니다.

---

## 🧠 프로젝트 목적

- 음악방송 점수 구성 요소를 중심으로 한 **정규화된 데이터베이스 구축**
- 팬덤이 전략을 수립할 수 있도록 **집계 쿼리 및 분석 지원**
- 회원 인증 기반의 **정보 접근 권한 관리**
- 게시판/댓글 시스템을 통한 **커뮤니티 기능 제공**

---

## 📅 프로젝트 일정표

| 주차        | 주요 내용                                                                 |
|-------------|---------------------------------------------------------------------------|
| 5~7주차     | 팀 구성                                                                  |
| 8~9주차     | 주제 탐색, 데이터 수집 (기존 주제 → 팬덤 중심으로 변경)                  |
| 10주차      | 개념적 설계: ER 다이어그램 작성                                           |
| 11주차      | 논리적 설계: 릴레이션 스키마 작성 및 정규화                                |
| 12주차      | 제약조건 및 키 설정, 초기 데이터 입력                                     |
| 13주차      | 무결성 검사 및 릴레이션 점검                                               |
| 14주차      | 통계/예측을 위한 쿼리 작성                                                |
| 15주차      | 최종 보고서 작성 및 테스트 완료                                            |

---

## 👥 팀 구성 및 기여도

| 팀원 | 역할 및 기여 |
|------|--------------|
| 상욱 | 릴레이션 스키마 정의, 데이터 구조 최적화 및 상세 편집 |
| 은영 | 주제 선정, ERD 작성, 문서화 및 진행 상황 정리        |
| 형민 | 데이터 수집 보조 및 릴레이션 구조 수정                |
| 나   | 전체 데이터 수집 및 가공, 부족한 샘플 데이터 생성      |

---

## 🔎 시스템 구조 요약

### 🎯 주요 기능

- 음악방송 1위 점수 예측을 위한 데이터 취합
- 게시글, 댓글 기반 커뮤니티 기능
- 인증 기반 회원제 시스템
- 실시간 순위 예측에 필요한 통계 조회 기능

### 🧱 데이터 모델링 요약

- 아티스트와 곡, 음반 관계 관리
- 날짜별 스트리밍 수 / 유튜브 조회수 / 음반 판매량 / 앱 투표수
- 사용자 등급별 권한 (관리자, 일반 회원, 가입 대기)
- 게시글 및 댓글의 삭제 여부 플래그 포함

---

## 🔨 ER 다이어그램 (개념적 설계)

![ERD](./ERD.png)

> ※ 실제 이미지 첨부 필요 (Draw.io, dbdiagram.io 등에서 작성 가능)

---

## 🧾 릴레이션 스키마 (논리적 설계)

- `Song(SongID, Artist, SongTitle, AlbumID)`
- `Album(AlbumID, AlbumTitle)`
- `StreamingData(SongID, Date, StreamingCount)`
- `AlbumSales(AlbumID, Date, SalesCount)`
- `YouTubeViews(SongID, Date, ViewCount)`
- `AppVotes(SongID, Date, VoteCount)`
- `Member(MemberID, Password, Nickname, MemberLevel, VerificationData)`
- `Post(PostID, PostTitle, Content, AuthorID, PostDate, Deleted)`
- `Comment(CommentID, PostID, Content, AuthorID, PostDate, Deleted)`

---

## 🧪 주요 구현 SQL

<details>
<summary><strong>CREATE TABLE 예시</strong></summary>

```sql
CREATE TABLE Song (
    SongID INT NOT NULL PRIMARY KEY,
    Artist VARCHAR(50) NOT NULL,
    SongTitle VARCHAR(50) NOT NULL,
    AlbumID INT,
    FOREIGN KEY (AlbumID) REFERENCES Album(AlbumID)
);
