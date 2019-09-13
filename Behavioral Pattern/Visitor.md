# 방문자(Visitor) - 객체 행동

* 의도: 객체 구조를이루는 원소에 대해 수행할 연산을 표현한다. 연산을 적용할 원소의 클래스를 변경하지 않고도 새로운 연산을 정의할 수 있도록 한다.
* 동기: 연산이 전체 클래스를 이루는 노드마다 분산되어 있어 유지보수 및 변경이 어렵다. -> 관련된 연산을 추려서 별도의 클래스로 묶어서 처리한다.
* 활용성
	* 다른 인터페이스를 가진 클래스가 객체 구조에 포함되어 있고, 구체클래스에 대해 달라진 연산을 이들 클래스의 객체에 대해 수행하고자 할 때
	* 관련되지 않은 여러 연산들이 한 객체 구조에 속한 객체들에 대해 수행될 필요가 있고, 이러한 연산들로 클래스를 더럽히고 싶지 않을 때
	* 객체구조를 정의한 클래스는 거의 변하지 않지만, 전체 구조에 걸쳐 새로운 연산을 정의하고 싶을때 -> 클래스 구조가 자주 변경된다면 클래스에 해당 연산을 정의하는 게 낫다.
* 구조
  ![Visitor](/img/Visitor.JPG) 
* 참여자
	* Visitor: 객체 구조 내에 있는 각 ConcreteElement 클래스를 위한 Visit() 연산을 선언한다. 이후 방문자는 Element가 제공하는 인터페이스를 통해 Element에 직접 접근할 수 있다.
	* ConcreteVisitor: Visitor에 선언된 연산을 구현한다. 각 연산은 대응되는 클래스에 정의된 일부 알고리즘을 구현한다. 또한 알고리즘이 운영될 수 있는 상황 정보를 제공하며, 자체 상태를 저장한다. -> 보통 순회 결과를 누적한다.
	* Element: 방문자를 인자로 받는 Accept() 연산을 정의한다.
	* ConcreteElement: Accept()를 구현한다.
	* ObjectStructure: 객체 구조내의 원소들을 나열한다. 방문자가 이 Element에 접근하게 하는 상위 인터페이스를 제공한다.
* 협력 방법
	* ConcreteVisitor 객체를 생성하고, 객체 구조를 따라서 각 원소를 방문하며 순회해야 합니다.
	* 구성 원소들을 방문할 때, 구성 원소는 해당 클래스의 Visitor연산을 호출한다. 이 원소들은 자신을 Visitor연산에 필요한 인자로 하여 필요시 원소에 직접 접근하도록 한다.
	![VisitorInteraction](/img/VisitorInteraction.JPG)  
* 결과
	* 새로운 연산을 쉽게 추가할 수 있다.
	* 관련된 연산은 방문자로 모이고, 관련 없는 연산은 따로 정의하게 한다.
	* 새로운 ConcreteElement 클래스의 추가는 어려워진다. ->새로운 ConcreteElement 클래스의 생성은 곧 모든 Visitor의 수정으로 이어진다.
	* 클래스 계층 구조에 걸쳐서 다양한 타입의 객체를 방문한다 -> Iterator가 같은 타입으로 구성된 것만 순회하던 것과 대비된다.
	* 상태를 누적한다 -> 방문자가 없다면 별도 인자로 전달되거나, 전역변수로 존재해야 한다.
	* 데이터 은닉을 깰 수도 있다.
* 구현
	* 이중 디스패치 - 실행되는 연산의 요청이 연산의 이름과 두 수신자의 타입에 따라 달라진다(여기서는 Visitor와 Element)
		* 단일 디스패치 - 실행되는 연산의 요청이 연산의 이름과 단일 수신자에 따라 달라진다.
	* 누가 객체 구조를 순회할 책임을 지는가?
		* 객체 구조: 재귀적인 Accept 호출로 순회한다.
		* 방문자: 객체 구조에 대한 연산 호출 결과에 따라 다른 순회 방법을 구현할 수 있다.
		* 별도의 반복자 객체: 재귀 동작이 없다면 이 편이 간편하다.
* 관련 패턴
	* 복합체 패턴
	* 해석자 패턴