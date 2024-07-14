---
tags:  
  - SOLID
  - SRP
  - OCP
  - LSP
  - ISP
  - DIP
  - Clean Architecture
---
#TIL 

_Original Document : [[SOLID_Private]]_
# 개요
**소프트웨어 설계에서 유지보수성과 확장성을 높이기 위해 설계 시 준수해야 할 기본 원칙.**
-  SOLID 원칙은 소프트웨어 설계에서 클래스의 배치와 서로간의 결합 방법을 정의하여, 보다 효과적인 시스템 아키텍처를 구축할 수 있도록 지침을 제공한다.
    ***
- 이 원칙들은 소프트웨어 구조를 변경에 유연하게 대응할 수 있도록 설계하며, 다양한 시스템에서 재사용할 수 있는 견고한 컴포넌트를 생성하는 것이 목적. 
	***
- SOLID 원칙을 따르는 것은 소프트웨어의 유지보수가 쉽고, 확장성이 높으며, 장기적인 관점에서 보다 효율적인 개발을 가능하게 한다.
***
# Single Responsibility Principle - SRP 
**하나의 클래스는 하나의 책임만 가져야 하며, 변경하는 이유는 오직 하나여야 한다.**
### 1. 단일책임과 변경의 이유
- SRP의 본질적인 의미는 함수 리펙터링과 달리 모듈 또는 클래스 수준에서의 책임 분리의 목적에 있다
	***
- 모듈이 변경되는 이유를 명확히 하고, 변경의 요구사항을 제시하는 actor를 한정하는 것이 핵심.

### 2. 응집도
- 응집도가 높다는 것은 모듈이 하나의 actor에 대해 책임을 진다는 것을 의미한다.
	 > 해당 변경을 요청하는 한 명 이상의 사람들을 가리킨다. 이러한 집단을 액터(actor)라고 부르겠다. 
	***
- 필요할 때 관련된 부분만을 집중적으로 수정할 수 있어 유지보수성의 증대를 기대할 수 있다.
### 3. 위반
##### 3.1 우발적 중복
1. 개발자가 각기 다른 기능 세가지 메서드를 하나의 클래스 안에 배치하여, 액터가 서로 결합된 상황.
2. 이 클래스에는 하나의 알고리즘을 공유하며, 서로 다른 액터를 책임지는 메서드가 a(), b()가 존재한다.
3. 업무를 할당 받은 개발자는 b() 메서드를 수정해야 하지만, 알고리즘이 공유 되고 있는 a() 메서드에 대해 알지 못해 a() 메서드에도 수정 사항이 반영되어 문제가 발생.
> ...서로 다른 액터가 의존하는 코드를 너무 가까이 배치했기 때문에 발생한다.
##### 3.2 병합
1. 개발자가 a() 메서드의 수정과 동시에 DBA가  해당 테이블 스키마를 수정하기 위해 두 개발자가 하나의 클래스를 체크아웃 받은 후 변경사항을 적용.
2. 변경 사항이 충돌해 병합이 발생.
> 최근 도구는 굉장히 뛰어나지만, 어떤 도구도 병합이 발생하는 모든 경우를 해결할 수 없다. 결국 병합에는 항상 위험이 뒤따르게 된다.
### 4.  해결
##### 데이터, 메서드 분리와 Facade Pattern
- 데이터 구조만 가지고 있는 클래스를 공유한다.
	- 각 클래스는 자신의 메서드에 필요한 요소만 코드만 포함하고 서로 존재를 모른다.
	- 분리된 클래스를 인스턴스화 하고 추적 해야하는 단점이 발생.
	***
- Facade Pattern
	- 간소화된 인터페이스를 제공한다.
	- 객체를 생성하며, 클라이언트의 요청을 적절한 서브시스템의 메서드로 전달하는 역할.
	***
- 중요도에 따른 Facade Pattern 
	- 기존 클래스와 직접적인 연관이 있는 메서드를 제외하고 개별 클래스로 분리 후, 기존 클래스를 퍼사드로 사용.
***
# OCP 
**소프트웨어의 구성 요소는 확장에 열려 있어야 하지만, 변경에 닫혀 있어야 한다.**
### 1. 확장과 변경
- 확장에 열려 있어야 한다.
	- 소프트웨어 구성 요소가 새로운 기능이나 요구 사항을 수용할 수 있도록 설계 되어야 한다.
		***
- 변경에 닫혀 있어야 한다.
	- 기존의 코드를 수정하지 않고, 확장을 수행할 수 있어야 함을 의미한다.
	- 검증된 기존 코드를 변경함으로써 발생할 수 있는 위험을 최소화.
### 2. 의존성 체계화 와 컴포넌트의 계층구조
##### 2.1 처리 과정을 클래스 단위로 분할하고, 클래스는 컴포넌트 단위로 분리
- Database
	- Financial Database
	- Financial Data Mapper
		- **Using**
			- Financial Database
			-  Financial entities
		- **Implement**
			- `<I>`Financial Data Gateway
		***
- Interactor
	-  `<I>`Financial Report Requester
	- Financial Report Generator
		- **Using**
			- Financial entities
			- `<I>`Financial Data Gateway
			- `<DS>`Financial Report Request
			- `<DS>`Financial Report Response 
		- **Implement**
			- `<I>`Financial Report Requester
	- Financial entities
	- `<I>`Financial Data Gateway
	- `<DS>`Financial Report Request
	- `<DS>`Financial Report Response 
		***
- Controller
	- Financial Report Controller
		- **Using**
			- `<I>`Financial Report Requester
			- `<DS>`Financial Report Request
			- `<DS>`Financial Report Response 
	- `<I>`Financial Report Presenter
		- **Using**
			- `<DS>`Financial Report Response 
		***
- Presenter
	- Screen
		- Screen Presenter
			- **Using**
				- `<DS>`Screen View Model
				- `<I>`Screen View
			-  **Implement**
				- `<I>`Financial Report Presenter
		- `<DS>`Screen View Model
		- `<I>`Screen View
			- **Using**
				- `<DS>`Screen View Model
	- Print
		- Print Presenter
			-  **Using**
				- `<DS>`Print View Model
				- `<I>`Print View
			- **Implement**
				- `<I>`Financial Report Presenter
		- `<DS>`Print View Model
		- `<I>`Print View
			- **Using**
				-  `<DS>`Print View Model
		***
- View
	- Web View
		- **Implement**
			- `<I>`Screen View
	- PDF View
		- **Implement**
			- `<I>`Print View
	***
- 단방향 의존성
	- 소프트웨어 구성 요소 간의 의존성은 단방향으로 이루어져야 한다. 그 이유는 컴포넌트 간 결합도를 낮추고 각 컴포넌트의 변경이 다른 컴포넌트에 미치는 영향을 최소화하기 위함이다.
		***
- 특정 수준 기반의 계층화
	- 시스템 내에서 각 계층은 특정 수준을 기반으로 조직화되어 구성 요소들을 체계적으로 관리하고, 각 계층의 독립성을 보장한다.
	- 높은 수준의 계층으로 갈수록, 보호받는 수준이 높아져, 핵심 비즈니스 로직이나 데이터 관리와 같은 중요한 기능이 외부의 변화로부터 격리할 수 있다.
***
# LSP
**자식 클래스는 부모 클래스를 대체할 수 있어야 한다.**
###  1. 확장과 치환
- 치환
	-  자식 클래스는 부모 클래스의 행위를 정확히 모방할 수 있어야 하며, 이를 통해 자식 클래스의 인스턴스를 부모 클래스의 인스턴스로 대체해 사용할 때 기존 코드의 정확성을 해치지 않아야 한다.
	- 코드 재사용의 목적을 넘어, 기존 코드의 호환성을 유지하면서 확장할 수 있는 설계가 되어야 한다.
- 상속의 확장
	-  상속을 통한 확장이 기능의 추가만을 의미하는 것이 아니라, 확장된 기능이 원래 클래스의 계약을 준수해야 한다는 것을 강조한다.
	- 부모 클래스를 사용하는 기존 클라이언트 코드를 변경하지 않고 자식 클래스의 인스턴스를 사용할 수 있어야 함을 의미.
### 2. 상속 가이드와 위반 사례
##### 2.1 LSP 를 준수하는 상속
- 계약에 의한 설계
	- 메서드가 지켜야 할 사전조건과 사후조건을 명확히 하여, 서브클래스에서 이를 확장만 할 수 있도록 한다.
		***
- 인터페이스 분리
	-  슈퍼클래스에 너무 많은 책임을 두지 않고, 필요에 따라 인터페이스를 분리하여 서브클래스가 구현해야 할 행동만을 정의한다.
##### 2.2 LSP 를 위반하는 상속 문제
- 메서드 오버라이딩과 치환
	- 서브클래스에서 슈퍼클래스의 메서드를 오버라이드하되, 예외를 추가로 발생시키거나 완전히 다른 동작을 구현하는 경우 서브클래스의 인스턴스로 슈퍼클래스의 인스턴스를 치환할 수 없다
***
# ISP
**클라이언트는 자신이 사용하지 않는 인터페이스에 의존하지 않아야 한다.**
### 1. 인터페이스 분리의 이유
- 각 인터페이스가 특정 클라이언트에게 필요한 동작만을 제공하여, 시스템 유연성을 증가시키고, 불필요한 의존성을 감소시키도록 사용하지 않는 메서드에 의존하지 않도록 분리해야한다.
### 2. 소스 코드의 의존성
- 큰 인터페이스 하나가 클라이언트에게 필요하지 않은 메서드까지 포함하게 되면, 클라이언트는 자신이 사용하지 않는 메서드에 대한 의존성을 갖게 된다.
***
# DIP
**고 수준 모듈은 저수준 모듈에 의존하지 않아야 하며, 모든 의존성은 추상화에 의존해야 한다.**
### 1. 추상에 의존하는 시스템
- 추상에 의존
	- 추상 클래스나 인터페이스 같은 추상화에 의존해야 한다.
	- 소스 코드가 구체적인 구현에 결박되지 않고, 유연하게 대응 가능.
	- 의존성 회피를 통해 시스템 결합도를 낮추고, 확장성과 유지보수성을 높인다.
		***
- 안정적인 의존
	-  DIP 의 주요 목적 중 하나는 변동성이 큰 구체적인 요소들에 대한 의존성을 최소화하는 것.
	- Java 의 String 클래스와 같이 안정적인 구현에 의존은 일반적으로 문제가 되지 않는다.
	- 널리 사용되고 그 안정성이 검증되어 있기 때문에 신뢰성을 보장할 수 있다.
### 2. 안정된 추상화와 변동성
>  1. **변동성이 큰 구체 클래스를 참조하지 말라.**
>  2. **변동성이 큰 구체 클래스로부터 파생하지 말라.**
>  3. **구체 함수를 오버라이드 하지 말라.**
>  4. **구체적이며 변동성이 크다면 절대로 그 이름을 언급하지 말라.**
### 3. 추상 팩토리와 구체 컴포넌트
- 추상 팩토리
	- 팩토리 인터페이스를 통해 서비스의 인스턴스 생성 메커니즘을 추상화.
	- 구체적인 클래스의 생성은 팩토리 구현 내부에서 이루어지며, 이 과정을 통해 시스템의 나머지 부분은 구체적인 클래스의 구현으로부터 독립적이게 된다.
	- 의존성을 팩토리 내부로 핞정함으로써 구현 변경에 따른 영향을 최소화.
		***
- 구체 컴포넌트의 제어 흐름과 의존성 역전
	-  제어의 흐름은 구체적인 구현에서 추상화된 인터페이스로 이동.
	- 의존성은 제어 흐름의 반대 방향으로 작동.
	- 즉, 고수준 구성 요소는 저수준 구성 요소의 구체적인 구현이 아닌 추상화된 인터페이스에 의존

***
# Ref:
Clean Architecture (p.62~98) - Robert C. Martin