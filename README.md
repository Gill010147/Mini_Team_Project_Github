# 요아정 가격 칼로리 계산 프로그램

## 📋 프로젝트 소개

**요아정 가격 칼로리 계산 프로그램**은 **MZ세대에게 인기 있는 요거트 아이스크림 브랜드 '요아정'**을 모델로 한 콘솔 기반 주문 시스템입니다. 이 프로젝트는 **초보 백엔드 개발자가 MVC 패턴과 Singleton 패턴을 학습하고 실습**하기 위해 직접 설계하고 구현한 미니 프로젝트입니다.

### 🎯 프로젝트 목표
- **MVC 패턴**의 이해와 실제 적용 경험 습득
- **Singleton 패턴**의 구현과 활용 방법 학습
- **객체 지향 프로그래밍**의 기본 원칙 적용
- **팀 협업**을 통한 코드 리뷰 및 개발 프로세스 경험

## 🍦 요아정 브랜드 배경

**요아정(요거트 아이스크림의 정석)**은 2021년 설립된 배달 전문 요거트 아이스크림 프랜차이즈로, 현재 전국 650여 개 매장을 운영하며 **배달 요거트 아이스크림 분야 점유율 1위**를 기록하고 있습니다. 

- **컨셉**: "EAT FRESH, EAT HEALTHY" - 맛과 건강을 모두 갖춘 건강한 디저트
- **특징**: 50여 종의 다양한 토핑으로 커스터마이징 가능한 요거트 아이스크림
- **타겟**: MZ세대를 중심으로 한 건강 디저트 선호 고객층

### 🗂️ 프로젝트 구조 (MVC 패턴 적용)

src/
- controller/
  - OrderController.java  # 주문 관련 비즈니스 로직 처리
  - MenuController.java   # 메뉴 관련 컨트롤러
- model/
  - Product.java          # 상품 정보 모델
  - Order.java            # 주문 정보 모델
  - Cart.java             # 장바구니 모델
- view/
  - MenuView.java         # 메뉴 출력 뷰
  - OrderView.java        # 주문 출력 뷰
  - MainView.java         # 메인 화면 뷰
- util/
  - SingletonManager.java # 싱글톤 패턴 구현


### 주요 기능

1. **상품 목록 조회**: 요아정의 다양한 요거트 아이스크림 메뉴 확인
2. **장바구니 기능**: 원하는 상품을 담고 수량 조절
3. **가격 계산**: 선택한 상품들의 총 가격 자동 계산
4. **칼로리 계산**: 각 상품의 칼로리 정보 제공 및 총 칼로리 계산
5. **주문 처리**: 최종 주문 확인 및 주문 완료 처리

## 🛠️ 기술 스택

- **언어**: Java 17
- **빌드 도구**: Maven
- **라이브러리**: Lombok (보일러플레이트 코드 줄이기)
- **디자인 패턴**: MVC Pattern, Singleton Pattern
- **개발 환경**: IntelliJ IDEA / Eclipse

## 👥 팀 구성

- **팀원**: 2명 ([@Gill010147](https://github.com/Gill010147), [@jihwan77](https://github.com/jihwan77))
- **개발 기간**: 2024.XX - 2024.XX
- **협업 방식**: GitHub을 통한 코드 리뷰 및 버전 관리

## 📚 학습 포인트

### 1. MVC 패턴 학습

**Model-View-Controller 패턴**을 실제 프로젝트에 적용하면서 다음과 같은 학습 효과를 얻었습니다:

- **관심사의 분리**: 데이터 처리(Model), 사용자 인터페이스(View), 비즈니스 로직(Controller)의 명확한 역할 구분
- **유지보수성 향상**: 각 계층이 독립적으로 동작하여 코드 수정 시 영향 범위 최소화
- **재사용성 증대**: Model과 View의 분리로 동일한 데이터를 다양한 방식으로 표현 가능

### 2. Singleton 패턴 학습

**싱글톤 패턴**을 통해 다음과 같은 개념을 학습했습니다:

- **인스턴스 관리**: 특정 클래스의 인스턴스가 오직 하나만 존재하도록 보장
- **메모리 효율성**: 객체 재사용을 통한 메모리 절약
- **전역 접근성**: 애플리케이션 전체에서 동일한 객체에 접근 가능

## 🔧 트러블슈팅

### 1. MVC 패턴 적용 시 발생한 문제점

**문제**: 초기 설계에서 Controller에 View 로직이 포함되어 MVC 패턴을 올바르게 적용하지 못함

**해결책**: 
- View 클래스에서만 사용자 인터페이스 관련 로직 처리
- Controller는 비즈니스 로직과 Model-View 간의 중재 역할에만 집중
- 각 계층 간의 의존성 방향을 명확히 정의 (Controller → Model, View / View → Model만 허용)

### 2. Singleton 패턴 구현 시 Thread Safety 문제

**문제**: 멀티스레드 환경에서 싱글톤 인스턴스가 중복 생성되는 문제 발생

**해결책**:
public class SingletonManager {
private static volatile SingletonManager instance;

text
private SingletonManager() {}

public static SingletonManager getInstance() {
    if (instance == null) {
        synchronized (SingletonManager.class) {
            if (instance == null) {
                instance = new SingletonManager();
            }
        }
    }
    return instance;
}
}

text
- **Double-checked locking** 패턴 적용으로 성능과 안전성 동시 확보
- **volatile** 키워드 사용으로 메모리 가시성 문제 해결

### 3. 데이터 일관성 문제

**문제**: 장바구니에 동일한 상품이 중복 추가되는 문제

**해결책**:
- HashMap을 활용한 상품 ID 기반 중복 관리
- 수량 증감 로직 분리로 데이터 일관성 보장

### 4. 사용자 입력 검증 미흡

**문제**: 잘못된 사용자 입력으로 인한 프로그램 오류 발생

**해결책**:
- try-catch 블록을 활용한 예외 처리
- 입력값 범위 검증 로직 추가
- 사용자 친화적인 오류 메시지 제공

## 🚀 실행 방법

1. **프로젝트 클론**
git clone https://github.com/Gill010147/Mini_Team_Project_Github.git
cd Mini_Team_Project_Github

text

2. **Maven 빌드**
mvn clean compile

text

3. **프로그램 실행**
java -cp target/classes Main

text

## 📖 향후 개선 사항

1. **데이터베이스 연동**: 현재 하드코딩된 메뉴 데이터를 DB로 이관
2. **GUI 구현**: 콘솔 기반에서 JavaFX 또는 Swing을 활용한 GUI 버전 개발
3. **결제 시스템**: 실제 결제 모듈 연동 (테스트 환경)
4. **주문 이력 관리**: 사용자별 주문 내역 저장 및 조회 기능
5. **단위 테스트**: JUnit을 활용한 테스트 코드 작성

## 🎓 학습 성과

이 프로젝트를 통해 다음과 같은 학습 성과를 얻었습니다:

- **디자인 패턴의 실무 적용**: MVC와 Singleton 패턴의 이론적 이해를 넘어 실제 구현 경험 습득
- **객체 지향 프로그래밍**: 캡슐화, 상속, 다형성 등의 OOP 원칙 적용
- **팀 협업**: Git/GitHub를 활용한 버전 관리 및 코드 리뷰 경험
- **문제 해결 능력**: 개발 과정에서 발생하는 다양한 문제 상황에 대한 해결 능력 향상

## 📞 문의사항

프로젝트에 대한 질문이나 피드백은 GitHub Issues 또는 이메일로 연락주세요.

- **GitHub**: [@Gill010147](https://github.com/Gill010147)
- **Project Repository**: [Mini_Team_Project_Github](https://github.com/Gill010147/Mini_Team_Project_Github)

*이 프로젝트는 **학습 목적**으로 제작되었으며, 실제 요아정 브랜드와는 관련이 없습니다.*
