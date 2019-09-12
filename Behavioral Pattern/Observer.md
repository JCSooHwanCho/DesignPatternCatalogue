# 감시자(Observer) - 객체 행동
* 의도:  객체 사이에 일대다 의존 관계를 두어, 객체상태가 변할 때 의존성을 가진 다른 객체들이 그 변화를 통지받고 자동으로 갱신될 수 있게 한다.
* 다른 이름: 종속자(Dependent),  게시-구독(Publish-Subscribe)
* 동기: 관련 객체들간의 일관성을 유지해야 하는데, 결합성을 높이고 싶지는 않다.
* 활용성
	* 어떤 추상 개념이 두 가지 양상을 갖고, 하나가 다른 하나에게 종속적일 때
	* 한 객체의 변화에 따라 다른 객체가 변해야 할 때, 그리고 프로그래머는 얼마나 많은 객체들이 변경되어야 하는지 몰라도 될 때
	* 어떤 객체가 자신의 변화를 통보하는데, 이 변화에 관심 있는 객체를 몰라도 될 때
* 구조
  ![Observer](/img/Observer.JPG) 
* 참여자
	* Subject: 감시자들을 알고 있는 주체, 감시자들을 붙이거나 떼내는 인터페이스 제공
	*  Observer: 주체에 생긴 변화에 관심 있는 객체를 갱신하는 데 필요한 인터페이스 정의
	* ConcreteSubject: ConcreteObserver 객체가 알려줘야 하는 상태 저장, 이 상태가 바뀌면 감시자에게 통보가 간다.
	* ConcreteObserver:  subject와 상태를 일관되게 유지하며, 이에 필요한 인터페이스 구현
* 협력 방법
	* ConcreceSubject는 Observer와의 일관성이 깨질만한 변경이 있을 때마다 Observer에게 통보한다.
	* Observer는 통보를 받으면 이 정보를 subject에 질의해서(혹은  통보할 때 Subject가 보내줘서) 얻어온다. 이 정보를 사용해서 상태를 일관되게 유지한다.
	![ObserverInteraction](/img/ObserverInteraction.JPG)  
* 결과
	* Subject와 Observer 클래스간에는 추상적인 결합만이 존재한다. -> 각자 따로 확장하는 것이 용이하다.
	* 브로드캐스트 방식의 교류를 가능하게 한다. 
	* 예측하지 못한 정보를 갱신할 수 있는 가능성이 있다. -> 무엇이 변했는지 알려면, 별도의 수단을 강구해야 한다.
* 구현
	* Subject와 Observer를 대응시킨다 -> 공간 절약을 위해 전체적으로 관리할 수도 있다.
	* 하나 이상의 Subject를 감시한다. -> 어떤 Subject에서 통보가 일어났는지 확인하려면, Subject가 자신을 담아서 보내야 한다.
	* 누가 갱신을 촉발할 것인가
		* Subject가 자동으로 한다. -> 사용자는 쓰기 편하지만, 변화가 잦은 경우에 비효율 적이다.
		* 사용자가 적절한 때에 한다. -> 효율적인 갱신이 가능하지만, 추가 인터페이스를 정의해줘야 하며 사용자가 이를 잊으면 오류가 발생한다.
	* 삭제한 Subject에 대한 참조를 유지하는 경우를 방지해야 한다(Dangling reference)
	* 통보 전에 Subject가 자체적으로 일관성을 유지해야 한다.
	* Observer마다 갱신 프로토콜이 다르면 안된다.
		* Push - Subject가 변경 정보를 Observer에 전달 -> Subject가 Observer의 필요를 알아야하므로, Observer가 Subject에게 드러나게 되며, 결과적으로 재사용성이 떨어진다.
		* Pull - Subject는 최소한으로 정보를 전달하고, Observer는 Subject에게 상세 정보를 요청함
	* 관심 있는 변경이 무엇인지 명확히 지정한다. -> 모든 변경에 대해서 Observer가 반응할 필요가 없는 경우, Observer는 자신을 등록할 때 관심있는 분야를 명시한다(Aspect라고 한다)
	* 복잡한 갱신의 의미 구조를 캡슐화한다. -> 별도의 갱신용 매니저 객체를 둔다
    	![ObserverChangeManager](/img/ObserverChangeManager.JPG)   
	* Subject와 Observer 클래스를 합친다.
* 관련 패턴
	* 중재자 패턴: ChangeManager가 중재자 역할을 한다.
	* 단일체 패턴: ChangeManager가 하나만 존재하게 한다.