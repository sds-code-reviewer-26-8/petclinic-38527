# CLAUDE.md

Spring Boot 기반 Petclinic REST 애플리케이션 (Java 17, Gradle Kotlin DSL).

## 기술 스택
- Spring Boot 4.1.1, Spring MVC (`spring-boot-starter-webmvc`), Spring Data JPA, Thymeleaf
- DB: H2 인메모리 (개발용 H2 console: `/h2-console`)
- API 문서: springdoc-openapi (`/swagger-ui.html`, `/v3/api-docs`)
- 테스트: JUnit 5 (`./gradlew test`)

## 빌드 / 실행
```bash
./gradlew bootRun      # 실행 (http://localhost:8080)
./gradlew build        # 빌드 + 테스트
./gradlew test         # 테스트만
```
Windows PowerShell에서는 `.\gradlew.bat` 사용. IDEA에서는 `PetclinicApplication` 실행 구성 사용.

## 패키지 구조 (`com.example.petclinic`)
- `controller/` — REST 컨트롤러 (Owner, Pet, PetType, Vet, Speciality, Visit, Member)
- `controller/response/` — 응답 DTO (`*Dto`)
- `service/` — 비즈니스 로직 (`*Service`)
- `repository/` — Spring Data JPA 리포지토리 (`*Repository`)
- `entity/` — JPA 엔티티 (Person 상위 클래스, Owner/Vet 등)
- `LoadDatabase` — 시작 시 초기 데이터 적재
- 설정: `src/main/resources/application.yml`

## 컨벤션
- 계층 흐름: Controller → Service → Repository. 컨트롤러에서 리포지토리를 직접 호출하지 않는다.
- 엔티티를 API로 직접 노출하지 않고 `controller/response`의 DTO로 변환해 반환한다.
- 새 도메인 추가 시 entity / repository / service / controller / dto를 기존 패턴에 맞춰 함께 만든다.
- 기존 코드의 네이밍·주석 밀도·스타일을 따른다.

## Git
- 원격: `origin` → https://github.com/sds-code-reviewer-26-8/petclinic-38527.git (브랜치 `main`)
- 커밋/푸시는 사용자가 요청할 때만 수행한다.
