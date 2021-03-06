#  템플릿 메소드(Template Method) - 클래스 행동

* 의도: 객체의 연산에는 알고리즘 뼈대만 정의하고, 구체적인 처리는 서브클래스로 미룬다. 알고리즘 구조 자체는 그대로 둔 채 알고리즘 각 단계 처리를 서브클래스에서 재정의하게 만든다.
* 동기: 프로그램마다 필요한 절차는 같지만 세부 동작을 다르게 하고 싶다.
* 활용성
	* 알고리즘에서 변하지 않는 부분은 한번 정의해놓고, 달라지는 부분만 서브클래스에서 정의하도록 남겨놓고자 할 때
	* 코드 중복을 피하고 싶을 때 -> 일반화를 위한 리팩토링
	* 서브클래스에서 확장을 제어할 수 있게 하고 싶을 때
* 구조
  ![TemplateMethod](/img/TemplateMethod.JPG) 
* 참여자
	* AbstractClass: 알고리즘 처리 단계 내의 기본 연산을 정의, 알고리즘의 뼈대를 구성하는 템플릿 메소드를 구현한다.
	* ConcreteClass: 서브클래스마다 달라지는 기본 연산을 구현한다.
* 협력 방법: Concrete는 Abstract를 통하여 알고리즘의 변하지 않는 처리단계를 구현한다.
* 결과
	* 라이브러리에 정의할 클래스들의 공통 부분을 분리한다.
	* 할리우드 원칙(부모 클래스에서만 서브 클래스의 연산을 호출할수 있게 한다)
	* 템플릿 메소드가 호출하는 연산
		* 구체 연산: ConcreteClass나 사용자 클래스에 정의된 연산
		* AbstractClass의 구체 연산: 서브 클래스에서 일반적으로 유용한 연산
		* 기본 연산: 추상화된 연산
		* 팩토리 메소드
		* 훅(Hook): 필요하다면 서브클래스에서 확장할 수 있는 기본 행동을 제공하는 연산. 기본적으로는 아무 내용도 없다.
	* 서브클래스를 정의할 때는 어떤 연산이 필수이고, 어떤 연산이 선택인지 반드시 알아야 한다.
* 구현
	* C++의 접근 제한 방법을 이용한다. -> 기본 연산은 protected로 구현하여, 템플릿 메소드만 호출하도록 한다. 기본 연산은 순수 가상함수로, 템플릿 메소드 자체는 비가상 멤버함수로 만든다.
	* 기본 연산의 수를 최소화한다.
	* 이름 짓는 규칙을 만든다 -> 재정의가 필요한 연산들은 식별이 잘 되도록 해야한다.
* 관련 패턴
	* 팩토리 메소드 패턴: 종종 템플릿 메소드 패턴이라고도 함
	* 전략 패턴: 상속을 이용하여 다양한 알고리즘을 만들어내는 것이 전략 패턴과 관련이 있다. 각 전략은 위임을 통하여 전체 알고리즘을 다양화한다.