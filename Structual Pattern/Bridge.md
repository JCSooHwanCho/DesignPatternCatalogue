#  가교(Bridge) - 객체 구조

* 의도 : 구현에서 추상을 분리하여, 이들이 독립적으로 다양성을 가질 ㅣ수 있도록 함
* 다른 이름 : 핸들/구현부(Handle/Body)
* 동기 : 상속을 이용하면  실제 구현에 대한 종속성이 증가하고, 확장이 어려워진다. -> 실제 구현을 담당하는 구현 클래스를 하나 두고, 이 클래스를 이용해 구현을 완성시킨다.
* 활용성
	* 추상적 개념과 이에 대한 구현 사이의 지속적인 종속 관계를 피하고 싶을 때
	* 추상적 개념과 구현 모두가 독립적으로 서브클래싱을 통해 확장되어야 할 때
	* 추상적 개념에 대한 구현 내용을 변경하는 것이 다른 관련 프로그램에 아무런 영향을 주지 않아야 할 때
	* (C++) 구현을 완벽하게 은닉하길 원할 때 -> 클래스를 구현하는 방식이 인터페이스에 모두 노출되기 때문!
	* 클래스 계통에서 클래스 수가 급증하는 것을 막고 싶을 때
	* 여러 객체들에 걸쳐 구현을 공유하고자 하며, 이런 사실을 사용자에게 공개하고 싶지 않을 때
* 구조
   ![bridge](/img/Bridge.JPG)
* 참여자
	* Abstraction: 추상적 개념에 대한 인터페이스를 제공하고, 객체 구현자에 대한 참조를 제공
	* RefindedAbstraction  추상적 개념에 정의된 인터페이스를 확장
	* Implementor: 구현 클래스에 대한 인터페이스를 제공한다. Abstraction에 정확하게 대응할 필요는 없다.
	* ConcreteImplementor: 인터페이스를 구현하는 것으로, 실질적인 구현 내용을 담는다.
* 협력 방법
	* Abstraction 클래스가 사용자 요청을  Implementor 객체에 전달한다.
* 결과
	* 인터페이스와 구현 분리 -> 런타임에 구현을 바꿀 수 있고, 구현이 바뀌어도 인터페이스 계통의 클래스는 재컴파일이 필요없다.
	* 확장성 재고 -> Abstraction과 Implementor를 독립적으로 확장할 수 있다.
	* 구현 세부사항을 사용자에게 숨긴다.
* 구현
	* Implementor는 하나만 둔다.
	* 정확한 Implementor 객체를 생성한다. -> 여러개의 Implementor 클래스가 있을 때, 이를 결정하는 방법이 필요하다.
		* 생성시 인자를 이용해 판단한다.
		* 초기에는 기본 구현을 사용하고, 필요에 따라서 다른 것을 선택한다.
		* 다른 객체에게 위임한다.
	* Implementor를 공유한다.
	* 다중 상속을 이용한다 -> 다만 상속을 쓰면 Bridge 패턴의 의미가 퇴색된다.
* 관련 패턴
	* 추상 팩토리 -> 특정 가교를 생성하고 복합할 수 있도록 합니다.
	* 적응자 패턴 -> 비슷하지만 도입되는 시점에서 차이가 있다
		* 적응자: 클래스 설계 이후
		* 가교: 클래스 설계 초기에 투입