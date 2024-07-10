
# Spring Boot 도서 관리 시스템

이 프로젝트는 Spring Boot 프레임워크를 사용하여 개발된 간단한 도서 관리 시스템입니다. JPA를 통한 데이터베이스 조작과 Thymeleaf를 이용한 웹 인터페이스를 제공합니다.

## 프로젝트 구조

```
src
├── main
│   ├── java
│   │   └── com
│   │       └── example
│   │           └── bootagitProject
│   │               ├── BootagitProjectApplication.java
│   │               ├── controller
│   │               │   └── BookController.java
│   │               ├── model
│   │               │   └── Book.java
│   │               ├── repository
│   │               │   └── BookRepository.java
│   │               └── service
│   │                   ├── BookService.java
│   │                   └── BookServiceImpl.java
│   └── resources
│       ├── application.properties
│       └── templates
│           └── books
│               ├── form.html
│               └── list.html
```

## 개발 환경 설정

1. JDK 11 이상 설치
2. Maven 3.6 이상 설치
3. MySQL 8.0 이상 설치 (또는 H2 데이터베이스 사용)

## 프로젝트 설정 및 실행

1. 프로젝트 클론
   ```
   git clone https://github.com/yourusername/bootagit-project.git
   cd bootagit-project
   ```

2. 데이터베이스 설정
   `src/main/resources/application.properties` 파일을 열고 다음과 같이 설정:
   ```
   spring.datasource.url=jdbc:mysql://localhost:3306/bookdb
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```

3. 프로젝트 빌드
   ```
   mvn clean install
   ```

4. 애플리케이션 실행
   ```
   mvn spring-boot:run
   ```

5. 웹 브라우저에서 `http://localhost:8080/books` 접속

## 주요 클래스 및 인터페이스

### Book.java
도서 정보를 나타내는 엔티티 클래스입니다.
```java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String author;
    private String isbn;
    // getters and setters
}
```

### BookRepository.java
JPA를 이용한 데이터베이스 조작을 위한 인터페이스입니다.
```java
@Repository
public interface BookRepository extends JpaRepository<Book, Long> {
}
```

### BookService.java 및 BookServiceImpl.java
비즈니스 로직을 처리하는 서비스 계층입니다.
```java
public interface BookService {
    List<Book> getAllBooks();
    Optional<Book> getBookById(Long id);
    Book saveBook(Book book);
    void deleteBook(Long id);
}

@Service
public class BookServiceImpl implements BookService {
    // 구현 내용
}
```

### BookController.java
웹 요청을 처리하는 컨트롤러입니다.
```java
@Controller
@RequestMapping("/books")
public class BookController {
    // 각 엔드포인트에 대한 메서드 구현
}
```

## Thymeleaf 템플릿

- `list.html`: 도서 목록을 표시합니다.
- `form.html`: 도서 추가 및 수정 폼을 제공합니다.

## API 엔드포인트

- GET `/books`: 모든 도서 목록 조회
- GET `/books/new`: 새 도서 추가 폼
- POST `/books/save`: 도서 저장/수정
- GET `/books/edit/{id}`: 도서 수정 폼
- GET `/books/delete/{id}`: 도서 삭제

## 개발 가이드라인

1. 코드 작성 시 Google Java Style Guide를 따릅니다.
2. 새로운 기능 개발 시 테스트 코드를 함께 작성합니다.
3. 커밋 메시지는 명확하고 간결하게 작성합니다.

## 문제 해결

1. 템플릿 관련 오류 발생 시:
   - 템플릿 파일의 경로와 이름이 올바른지 확인
   - Thymeleaf 문법 오류 확인
   - `application.properties`에 템플릿 설정이 올바른지 확인

2. 데이터베이스 연결 오류:
   - MySQL 서비스가 실행 중인지 확인
   - `application.properties`의 데이터베이스 설정 확인
   - 필요한 데이터베이스와 테이블이 생성되었는지 확인

3. 빌드 오류:
   - Maven 의존성이 올바르게 다운로드되었는지 확인
   - `mvn clean`을 실행한 후 다시 빌드

## 향후 개선 계획

1. 입력 데이터 유효성 검사 추가
2. 페이지네이션 구현
3. 도서 검색 기능 추가
4. 사용자 인증 및 권한 관리 시스템 구현
5. RESTful API 확장

## 기여 방법

1. 이슈를 생성하여 새로운 기능이나 버그를 제안합니다.
2. 포크 후 새 브랜치에서 개발을 진행합니다.
3. 테스트를 실행하고 코드 스타일을 확인합니다.
4. Pull Request를 생성하여 변경 사항을 제안합니다.

