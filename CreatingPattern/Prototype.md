# 원형(Prototype) - 객체 생성(Object Creational)

* 의도 : 원형이 되는 인스턴스를 사용하여 생성할 객체의 종류를 명시하고, 이렇게 만든 견본을 복사해서 새로운 객체를 생성한다.
* 동기 : 프레임워크 레벨의 도구가 좀 더 다양한 요소를 다루도록 하고 싶다.
* 활용성
	* 제품의 생성, 복합, 표현 방법에 독립적인 제품을 만들고자 할 때
	* 인스턴스화할 클래스를 런타임에 지정할 때(동적 로딩)
	* 제품 클래스 계통과 병렬적으로 만드는 팩토리 클래스를 피하고 싶다.
	* 클래스의 인스턴스들이 서로 다른 상태 조합 중의 하나일 때
* 구조
   ![Prototype](/img/Prototype.JPG)
* 참여자
	* Prototype : 자신을 복제하는데 필요한 인터페이스를 정의한다.
	* ConcretePrototype :  자신을 복제하는 연산을 구현한다.
	* Client : 원형에 자기 자신의 복제를 요청하여 새로운 객체를 생성한다.
* 협력 방법
	* 사용자는 원형 클래스에 스스로를 복제하도록 요청한다.
* 결과 -> 추상 팩토리 및 빌더와 비슷함
	* 런타임에 새로운 제품을 추가하고 삭제할 수 있다.
	* 값들을 다양화함으로 새로운 객체를 명세한다.  -> 클래스 정의를 대폭으로 줄여준다.
	* 구조를 다양화함으로써 새로운 객체를 명세할 수 있습니다. 
	* 서브클래스의 수를 줄인다. -> 팩토리 메소드와 대비되는 부분으로, Product가 늘어도 Creator가 늘어나지 않는다.
		* 1급 객체를 처리하지 않는 언어에서 이득을 본다.
	* 동적으로 클래스에 따라 응용프로그램을 설정할 수 있다. -> 동적으로 클래스를 등록할 수 있도록 해주는 일부 런타임에서 유용(C++ 등)
	* 원형의 서브클래스가 clone()연산을 구현해야만 한다 -> 이미 만들어져서 수정이 안되거나, 복사가 지원이 안된다거나, 순환참조가 있다던가...
* 구현 -> 정적 언어에서 유용하다. 런타임에 타입 정보가 거의 없기 때문에 -> 동적 언어에서는 중요하지 않다.
	* 원형 관리자를 사용한다. -> 원형의 수가 정해지지 않은 경우에는 이를 동적으로 관리할 주체가 필요하다.
	* clone() 연산을 구현한다. -> 얕은 복사 vs 깊은 복사
	* 복사한 clone을 초기화합니다 -> setter, intialize 등의 메소드를 제공해야 한다.
	* Clone() 으로 반환된 인스턴스는 다운캐스팅하지 않고도 쓸 수 있어야 한다.
* 관련 패턴
	* 추상 팩토리 - 비슷한 패턴이나, 상호 협력적으로도 사용 가능
	* 복합체 패턴
	* 장식자 패턴