# 2장 타입

### 2.1 타입이란

1. 자료형으로서의 타입
    
    자바스크립트는 7가지 데이터 타입을 정의한다
    
    - undefined
    - null
    - Boolean
    - String
    - Symbol
    - Numeric(Number, BigInt)
    - Object
    
2. 집합으로서의 타입
    
    타입은 값이 가질 수 있는 유효한 범위의 집합을 말한다
    
    타입을 제한하면 타입스크립트 컴파일러는 함수를 호출할 때 호환되는 인자로 호출했는지 판단한다
    
    이때 올바르지 않은 타입의 값으로 함수를 호출 했을 때 타입스크립트 컴파일러는 에러를 발생시킨다.
    
    1. 정적타입과 동적타입
        
        타입을 결정하는 시점에 따라 정적타입, 동적타입으로 분류할 수 있다.
        
        - 정적타입: 모든 변수의 타입이 컴파일타임에 결정 ex) C, 자바, 타입스크립트
        - 동적타입: 변수타입이 런타임에서 결정 ex) 파이썬, 자바스크립트
        
    2. 강타입과 약타입
            - 암묵적 타입 변환: 타입을 명시하지 않았지만 컴파일러 또는 엔진 등에 의;해 런타임에 타입이 자동으로 변경되는 것
            - 강타입 언어는 서로 다른 타입을 갖는 값끼리 연산 시도시 컴파일러나 인터프리터에서 에러 발생 ex) 파이썬, 루비, 타입스크립트
            - 반면 약타입 언어는 컴파일러나 인터프리터가 내부적으로 판단해서 특정 값의 타입을 변환하여 연산을 수행 후 값 도출 ex) C++, 자바, 자바스크립트
            - 타입시스템: 타입 검사기가 프로그램에 타입을 할당하는 데 사용하는 규칙 집합으로, 크게 두가지로 분류한다. 타입을 컴파일러에 명시적으로 알려줘야 하는 타입 시스템, 자동으로 타입을 추론하는 타입 시스템
        
            
        
### 2.2 타입스크립트의 타입 시스템
        
1. 타입 애너테이션
            
    변수나 상수 혹은 함수의 인자와 반환 값에 타입을 명시적으로 선언해서 어떤 타입 값이 저장될 것인지 컴파일러에 알려주는 문법
            
    타입스크립트는 변수 이름뒤에 : type 구문을 붙여 데이터 타입 명시
2. 구조적 타이핑
            
    타입은 이름으로 구분되며 컴파일 타임 이후에도 남아있다. 이것을 명목적으로 구체화한 타입 시스템이라고 부르기도 한다.
            
    그러나 이름으로 타입을 구분하는 명목적인 타입 언어의 특징과 달리 타입스크립트는 구조로 타입을 구분 → 구조적 타이핑
3. 구조적 서브타이핑
                
    구조적 서브타이핑이란 객체가 가지고 있는 속성을 바탕으로 타입을 구분하는 것. 이름이 다른 객체라도 속성이 동일하다면 타입스크립트는 서로 호환이 가능한 동일한 타입으로 여긴다.
                
                ```tsx
                interface Pet {
                name: string;
                }
                
                interface Cat {
                name: string;
                age:number;
                
                }
                
                let pet: Pet;
                let cat:Cat = {name:'kitty'; age:1}
                
                pet = cat // Cat과 Pet이 각각 다른 타입으로 선언되었지만 cat을 pet에 할당할 수 있다
                ```
                
            
        구조적 서브타이핑은 함수의 매개변수에도 적용된다.
            
    4. 자바스크립트를 닮은 타입스크립트
                
        타입스크립트가 구조적 타이핑을 채택한 이유는 타입스크립트가 자바스크립트를 모델링한 언어이기 때문이다. 자바스크립트는 본질적으로 덕 타이핑을 기반으로 한다.
                
        - 덕타이핑: 어떤 함수의 매개변숫값이 올바르게 주어진다면 그 값이 어떻게 만들어졌는지 신경쓰지 않고 사용한다는 개념이다.
                
        자바스크립트는 런타임에 타입을 검사하는 덕타이핑 언어. 반면 타입스크립트는 컴파일타임에 타입체커가 타입을 검사하는 구조적타이핑 언어이다.
                
    5. 구조적 타이핑의 결과
                
        객체에 속성이 갑자기 추가될 때 타입을 확정할 수 없어 에러를 발생시키는 경우가 있다., 이러한 한계를 극복하고 타입스크립테 명목적 타이핑 언어의 특징을 가미한 식별할 수 있는 유니온 같은 방법이 생겨났다.
                
    6. 타입스크립트의 점진적 타입 확인
        - 점진적 타입 검사: 컴파일 타임에 타입을 검사하면서 필요에 따라 타입 선언 생략을 허용하는 방식
                    
                    ```tsx
                    function add(x, y) { return x+y }
                    
                    //아래와 같이 암시적 타입 변환
                    function add(x: any, y: any): any;
                    ```
                    
        - 타입스크립트는 자바스크립트의 슈퍼셋 언어이므로 타입을 지정하지 않은 자바스크립트 코드를 타입스크립트로 마이그레이션할 때 타입스크립트의 점진적 타이핑이라는 특징을 유용하게 활용할 수 있다.
                    
            
    7. 자바스크립트의 슈퍼셋
            
        타입스크립트 컴파일러는 일반 자바스크립트 프로그래에서도 유용하게 사용할 수 있다.
            
            ex) 타입추론으로 잘못된 메서드 사용 시 메서드 대체 제안 등
            
    8. 값 vs 타입
                
        타입스크립트에서 값은 타입선언 혹은 as로 작성하고 값은 할당연산자 = 로 작성한다.
                
        구조분해할당 사용시 주의하여 작성 
                
                ```tsx
                function email({
                person,
                subject, 
                body}:{
                person: Person, 
                subject: string, 
                body: string})
                {}
                ```
                
         - 타입스크립트에서 클래스는 타입으로도 사용된다. 즉, 클래스는 값과 타입 공간 모두에 포함될 수 있다.
         - enum도 클래스처럼 타입 공간에서 타입을 제한하는 역할을 하지만 자바스크립트 런타임에서 실제 값으로 사용될 수 있다.
                
                ```tsx
                // enum이 타입으로 사용된 예
                enum WeekDays {
                 MON = 'mon',
                 TUES = 'tues' .
                 //..,.,
                 }
                 
                 type WeekDaysKey = keyof typeof WeekDays
                 function printDay(key: WeekDaysKey, message: string){
                 const day = WeekDays[key]
                 if(day<= WeekDays.TUES){
                	 console.log('it's still ${day}day, ${message}
                 }
                 }
                 
                 
                 //enum이 값으로 사용된 예
                 enum Color {
                 BLUE: "3242",
                 MINT: "4324"
                 }
                 
                 function whatMintColor(palette:{MINT: string}){
                 return palette.MINT
                 }
                ```
                
                - enum의 단점
                    - 트리쉐이킹이 되지 않아 번들 사이즈에 영향
                        - const enum
                            - as const

9. 타입을 확인하는 방법
    - typeof, instanceof

### 2.3 원시타입

- boolean
- undefined
- null
- number (NaN, Infinity 포함)
- bigint
- string
- symbol

null과 undefined의 경우 tsconfig나 사용자 취향에 따라 다르게 사용될 여지가 있다.

strictNullChecks 옵션 활성화한 경우 사용자가 명시적으로 null이나 undefined를 포함해야 해당 두개를 사용할 수 있다.

그렇지 않으면 에러가 발생하는데, 보통 타입가드로 걸러내거나 !로 단언

### 2.4 객체타입

- object
- {}
- array
    - Array keyword or []
- type, interface
- function
- 호출시그니처를 사용하여 함수자체의 타입을 지정