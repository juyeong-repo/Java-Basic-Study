자바는 객체지향언어이고, 이 언어는 객체를 부품화하는데 이때 이 부품에 다양한 타입을 대입하여 각각 다른 결과물을 도출해내는 특징을 '다형성'이라 한다.
자바의 상속과 인터페이스는 이 다형성을 극대화하는 기능이다. 
extends, implements를 큰 생각없이 습관적으로 쓰다가, 이렇게 들여다보니 결국 다형성의 개념과 맞닿는 기능임이 흥미로웠다. 

# 7. 상속
상속 : 부모가 자식에게 물려주는 행위
- 부모 클래스의 멤버를 자식 클래스에게 물려줄 수 있다.
- class 자식 extends 부모
- 코드의 중복을 막고, 클래스의 수정을 최소화하며 유지보수 시간을 줄인다. 
- 상속 시 부모의 모든 필드,메소드를 물려받는 것은 아니고 private 접근 제한은 제외된다.
- 자바는 다중 상속을 허용하지 않는다.



## 부모 생성자 호출
- 자식 객체를 생성하면 부모 객체가 먼저 생성되고 자식 객체가 그 다음에 생성된다.
- 모든 객체는 클래스의 생성자를 호출해야만 생성되는데, 부모 생성자를 어디서 호출했냐면.. 바로 super(); 얘다. 
- 생략가능하지만, 부모클래스에 기본 생성자가 없고 매개변수가 있는 생성자만 있다면
- 자식클래스에서도 명시적으로 super(매개변수, , ...) 라고 호출해야 한다.

## 메소드 재정의
1. 부모 클래스의 모든 메소드가 자식 클래스에 맞게 설계되어 있다면, 가장 이상적이지만 어떤 메소드는 자식 클래스가 사용하기에 적합하지 않을 수도 있다.
2. 이 경우 상속된 일부 메소드는 자식 클래스에서 다시 수정해서 사용해야 한다.
3. 이런 경우를 위해 메소드 오버라이딩 기능을 제공한다.
-> 자바에선 @Override 사용
4. 자식 클래스에서 부모 클래스의 메소드를 오버라이딩하게 되면, 부모 클래스의 메소드는 숨겨지고 오버라이딩 된 자식 메소드만 사용된다. 부모 클래스 메소드를 호출하고 싶다면 super.부모메소드(); 하면 됨


## final 클래스와 final 메소드
- 클래스/메소드 선언 시에 final 키워드를 붙이면 상속과 관련이 있다.
- 클래스 선언시 final 키워드를 붙이면 최종적인 클래스 이므로 상속할 수 없다.
- 메소드 선언 시 final 키워드를 붙이면, 이 메소드는 최종적인 메소드이므로, 오버라이딩할 수 없는 메소드가 된다.

## protected 접근 제한자 (필드, 생성자, 메소드 선언에 사용)
- protected는 public과 default의 중간 쯤이다.
- 같은 패키지에서는 default와 같이 접근 제한이 없음
- 다른 패키지에서는 자식 클래스만 접근을 허용한다. (이게 포인트!)

## 타입변환과 다형성
다형성은 같은 타입이지만 실행 결과가 다양한 객체를 이용 할 수 있는 성질을 말한다.
하나의 타입에 여러 객체를 대입함으로써 다양한 기능을 이용할 수 있도록 해준다.
다형성을 위해 자바는 부모 클래스로 타입 변환을 허용한다.
즉, 부모 타입에 모든 자식 객체가 대입 될 수 있다.
이 떄, 역시 자식타입이 부모타입으로 강제 타입 변환 (Casting) 될 수 있고, 이땐 뭘로 확인해야겠어
바로 instanceof 👍 

 ```
boolean result = 좌항(객체) instanceof 우항(타입)

public vod method(Parent parent){
	if(parent istnaceof Child){ //강제 타입 변환 가능 : True , false 로 반환
    	Child child = (Child) parent;
    }
}
 ```




## 추상클래스
추상은 실체 간에 공통되는 특성을 추출한 것이고 객체를 직접 생성할 수 있는 클래스를 실체 클래스라고 한다.
추상 클래스와 실체 클래스는 상속의 관계를 가지고 있다.
추상 클래스는 새로운 실체 클래스를 만들기 위해 부모 클래스로만 사용된다.

### 추상 클래스의 용도
1. 실체 클래스들의 공통된 필드와 메소드의 이름을 통일할 목적
핸드폰 클래스를 설계한다 하면, 
- 필드명 불일치
    Telephone 클래스에선 owner, SmartPhone에서는 user라고 저장
- 메소드명 불일치
    Telephone 클래스에선 powerOn(), SmartPhone에서는 turnOn()
이렇게 공통된 필드와 메소드 이름을 통일 하기 위해 사용한다.

2. 실체 클래스 작성시 시간 절약
공통 필드/메소드는 추상 클래스인 Phone에 모두 선언하고, 실체 클래스마다 다른 점만 선언하게 되면, 실체 클래스 작성시에 시간을 절약 할 수 있다.
즉 추상 클래스는 설계 규격의 역활을 하게 된다.
 ```
public abstract class 클래스{
	//필드
    //생성자
    //메소드
}
 ```
- 자식 클래스에서 추상 메소드를 Override하지 않는다면 에러가 발생한다.


# 8. 인터페이스
## 인터페이스
- 객체의 사용방법을 정의한 타입
- 자바의 람다식은 함수적 인터페이스의 구현 객체를 생성하기 때문에 인터페이스의 중요성은 더욱 커졌다 :) 
- ![인터페이스](https://velog.velcdn.com/images/petit-prince/post/75d06b39-04b8-4c4c-8f22-a92d22286776/image.png)
- 개발코드를 수정하지 않고, 사용하는 객체를 변경할 수 있도록 하기 위해 인터페이스를 중간에 둔다. -> 이게 넘 재밌었다
- 하나의 객체가 아니라, 여러 객체들과 사용이 가능하므로 어떤 객체를 사용하느냐에 따라ㅏ 실행내용과 리턴값이 다를 수 있다. 따라서 개발코드측면에서 코드 변경 없이 실행 내용과 리턴값을 다양화할 수 있다. 

## 인터페이스 선언
 ```
interface 인터페이스 명{
	//상수
    타입 상수명 = 값;
    //추상 메소드
    타입 메소드명(매개변수, ...);
    //디폴트 메소드
    default 타입 메소드명(매개변수,...){...}
    //정적 메소드
    static 타입 메소드명(매개변수){...}
}
 ```

- 상수 필드(Constant Field)
1) 인터페이스는 객체 사용 설명서이므로 런타임 시 데이터를 저장할 수 있는 필드를 선언할 수 없다. 그러나 상수 필드는 가능하다. 반드시 초기값을 대입해야 한다.

- 추상 메소드(Abstract Method)
1) 추상 메소드는 객체가 가지고 있는 메소드를 설명한 것 (어떤 매개값이 필요한지, 리턴값이 무엇인지만 알려줌)
2) 실제 실행은 객체가 가진다.
- 디폴트 메소드(Default Method)
1) 인터페이스에 선언되지만, 사실은 객체가 가지고 있는 인스턴스 메소드라고 생각하면된다
2) 인터페이스 구현한 객체A,B가 있다고 가정할 때, 인터페이스에 디폴트 메소드를 둠으로서 A,B 둘다 수정할 필요가 없어짐
- 정적 메소드(Static Method)
1) 디폴트 메소드와 달리 객체가 없이 인터페이스만으로 호출 가능

## 상수 필드 선언
- 상수는 public static final로 선언하는데, 인터페이스의 필드는 모두 public static final이기에 안붙여도 자동적으로 붙게 된다.
```
interface 인터페이스 명{
public static final MAX_VALUE = 값;
}
 ```
 - 상수명은 대문자로, 서로 다른 단어로 구성된 경우 언더바로 연결하는 것이 관례
 
 ```
public interface RemoteControl{
    // static final을 안붙여도 인터페이스의 필드는 상수이다.
	public static final int MAX_VOLUME = 10;
    public int MIN_VOLUME = 0;
}
 ```
 
 
### 추상 메소드 선언 
인터페이스를 통해 호출되는 메소드는, 최종적으로 객체에서 실행된다 -> 인터페이스 메소드에는 실행블록이 없다.
###  디폴트 메소드 선언
default 키워드가 리턴 타입 앞에 붙는다. 생략해도 컴파일 과정에 붙음
### 정적 메소드 선언
클래스의 정적 메소드 선언과 동일


 ```
    // 상수
	int MAX_VOLUME = 10;
    int MIN_VOLUME = 0;
    
    // 추상 메소드
    void turnOff();
    void turnOn();
    void setVolume(int volume);
    
    //디폴트 메소드
    default void setMute(boolean mute){
    	if(mute){
        	sout("무음처리");
        }
        else{
        	soutv("무음 해제");
        }
    }
    //정적 메소드
	static void changeBattery(){
    	sout("건전지를 교체합니다.");
	}
 ```
 
## 인터페이스 구현
개발 코드가 인터페이스를 호출하면, 인터페이스는 객체의 메소드 호출
객체는 정의된 추상 메소드와 동일한 메소드 이름,매개타입,리턴타입을 가진 실체메소드를 가지고 있어야 한다.
구현 객체를 생성하는 클래스를 구현 클래스라고 한다. 

### 구현클래스

 ```
  public class Television implements RemoteControl{
	//필드
    private int volume;
    
    //turnOn() 추상메소드의 실체 메소드
    public void turnOn(){
    	sout("티비를 켭니다");
    }
    //Keep implements...
}
 ```
 - 인터페이스의 모든 메소드는 기본적으로 public 접근 제한을 갖기 때문에 public보다 더 낮은 접근 제한으로 작성할 수 없다.
- 만약 인터페이스에 선언된 추상 메소드에 대응하는 실체 메소드를 구현 클래스가 작성하지 않으면 구현 클래스는 자동적으로 추상 클래스가 된다. -> abstract키워드를 추가해야 한다.

### 익명 구현 객체
구현 클래스를 만들어 사용하는 것이 일반적이고, 클래스 재사용성 때문에 편리하지만, 일회성 구현 객체를 만들기 위해 소스파일과 클래스를 선언하는 것은 비효율적이다.
이를 위해 익명 구현 객체가 존재한다.
람다식은 인터페이스의 익명 구현 객체를 만든다 -> 
 ```
인터페이스 변수 = new 인터페이스(){
	//인터페이스에 선언된 추상 메소드의 실체 메소드 구현
};

 ```
### 다중 인터페이스 implements
- ![다중 인터페이스 구현](https://velog.velcdn.com/images/petit-prince/post/3e742e02-e593-462e-aa18-85716d8c17c2/image.png)
 ```
public class 구현클래스명 implements 인터페이스A, 인터페이스B{
	//인터페이스A에 선언된 추상 메소드의 실체 메소드 선언
    //인터페이스B에 선언된 추상 메소드의 실체 메소드 선언
}

 ```
## 인터페이스 사용
- 인터페이스로 구현 객체를 사용하려면, 인터페이스 변수에 구현 객체를 대입한다.
- 인터페이스 변수는 참조 타입이기에, 구현 객체의 번지를 저장한다.
- 개발 코드에서 인터페이스는 클래스의 필드, 생성자 또는 메소드의 매개 변수, 생성자 또는 메소드의 로컬 변수로 선언될 수 있다.
 ```
public class MyClass{
	//필드
	RemoteControl rc = new Television();
    
    //생성자
    MyClass(RemoteControl rc){
    	this.rc = rc;
	}
    
    //메소드 
    void methodA(){
    	RemoteControl rc = new Audio();
	}
    
    void methodB(RemoteControl rc){...}
    //...
    
    mc.methodB(new Audio());
    
}
 ```
## 타입변환과 다형성
상속은 같은 종류의 하위 클래스를 만드는 기술 , 인터페이스는 사용 방법이 동일한 클래스를 만드는 기술이다.
둘의 개념적 차이가 존재하지만, 둘 다 다형성을 구현한다. 다형성 다형성 신나는 노래🥳
- 인터페이스의 다형성이란?
: 프로그램 소스는 변함이 없는데, 구현 객체를 교체함으로써 프로그램의 실행 결과가 다양해 진다. 당연히 유지보수에 좋다. 
- 구현 객체가 인터페이스 타입으로 자동 변환하면, 인터페이스 메소드만 사용 가능하다. 경우에 따라, 구현 클래스에 선언된 필드/메소드를 사용해야 할 경우도 있다. 이때 강제 타입 변환으로 다시 구현 클래스타입으로 변환 후, 구현 클래스의 필드/메소드를 사용할 수 있다. -> instacneof 를 사용하여 객체 타입 확인하기~
  
 ```
public void dirve(Vehicle vehicle){
  if(vehicle instanceof Bus){
		Bus bus = (Bus) vehicle;
  }
}
 ```

## 인터페이스 상속
- 인터페이스는 인터페이스를 상속할 수 있다.
- 인터페이스는 다중 상속이 가능하다.

 ```
  public class Television implements RemoteControl{
	//필드
    private int volume;
    
    //turnOn() 추상메소드의 실체 메소드
    public void turnOn(){
    	sout("티비를 켭니다");
    }
    //Keep implements...
}
 ```
 - 인터페이스의 모든 메소드는 기본적으로 public 접근 제한을 갖기 때문에 public보다 더 낮은 접근 제한으로 작성할 수 없다.
- 만약 인터페이스에 선언된 추상 메소드에 대응하는 실체 메소드를 구현 클래스가 작성하지 않으면 구현 클래스는 자동적으로 추상 클래스가 된다. -> abstract키워드를 추가해야 한다.

### 익명 구현 객체
구현 클래스를 만들어 사용하는 것이 일반적이고, 클래스 재사용성 때문에 편리하지만, 일회성 구현 객체를 만들기 위해 소스파일과 클래스를 선언하는 것은 비효율적이다.
이를 위해 익명 구현 객체가 존재한다.
람다식은 인터페이스의 익명 구현 객체를 만든다 -> 
 ```
인터페이스 변수 = new 인터페이스(){
	//인터페이스에 선언된 추상 메소드의 실체 메소드 구현
};

 ```
### 다중 인터페이스 implements
- ![다중 인터페이스 구현](https://velog.velcdn.com/images/petit-prince/post/3e742e02-e593-462e-aa18-85716d8c17c2/image.png)
 ```
public class 구현클래스명 implements 인터페이스A, 인터페이스B{
	//인터페이스A에 선언된 추상 메소드의 실체 메소드 선언
    //인터페이스B에 선언된 추상 메소드의 실체 메소드 선언
}

 ```
## 인터페이스 사용
- 인터페이스로 구현 객체를 사용하려면, 인터페이스 변수에 구현 객체를 대입한다.
- 인터페이스 변수는 참조 타입이기에, 구현 객체의 번지를 저장한다.
- 개발 코드에서 인터페이스는 클래스의 필드, 생성자 또는 메소드의 매개 변수, 생성자 또는 메소드의 로컬 변수로 선언될 수 있다.
 ```
public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스1 {...}
}
 ```
1) 하위 인터페이스를 구현하는 객체는 하위 메소드 뿐 아니라 상위 인터페이스의 모든 추상 메소드에 대한 실체 메소드를 가지고 있어야 한다.
2) 하위 인터페이스 타입은 상, 하위 인터페이스 메소드 사용이 가능하다.
3) 그러나 상위 인터페이스는 상위 메소드만 사용 가능하다.

## 디폴트 메소드와 인터페이스 확장
부모 인터페이스에 디폴트 메소드가 정의 되어 있을 경우, 자식 인터페이스에서 디폴트 메소드를 활용하는 방법은 세가지다.

디폴트 메소드를 단순히 상속만 받는다.
디폴트 메소드를 재정의(Override)해서 실행 내용을 변경한다.
디폴트 메소드를 추상 메소드로 재선언한다.
