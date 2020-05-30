># NAVER D2
>### 참고 : <https://d2.naver.com/helloworld/1329>
>>### 열공하자! ㅎㅎ

> "지극히 개인적이고 주관적인 판단 기준을 먼저 밝힌다면, 가비지 컬렉션(Garbage Collection, 이하 GC)에 대해
잘 알고 있을수록 실력이 좋은 Java 개발자라고 생각합니다!"

> "GC 과정에 관심을 가질 정도라면, 규모가 일정 이상인 애플리케이션을 제작해 본 경험이 있을 것입니다.
또, 어떤 GC 알고리즘을 선택할 것인지 고민할 정도면 스스로 제작한 애플리케이션의 특징을 정확히
이해하고 있다고 볼 수 있습니다."

-----------

### 가비지 컬렉션 과정 - Generational Garbage Collection
1. 'stop-the-world' <br>
stop-the-world란, GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것이다. <br>
stop-the-world가 발생하면, GC를 실행하는 Thread를 제외한 나머지 Thread는 모두 작업을 멈춘다. <br>
어떤 GC알고리즘을 사용하더라도 stop-the-world는 발생한다. but 시간을 줄일 수 있다(GC 튜닝)

2. Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않는다. - null로 바꿔주는게 최선(또는 
System.gc() 호출 but 성능에 매우 큰 영향을 끼친다 - 절대 사용하지 마라!)

3. NOT 개발자가 메모리를 명시적으로 해제 BUT 가비지 컬렉터가 지운다. <br>
    ## 가비지 컬렉터의 기반이 되는 두 가지 가설!- <br>
    - 대부분의 객체는 금방 접근 불가능한 상태(unreachable)가 된다
    - 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다. <br>
 -> 이러한 가설을 'weak generational hypothesis'라 한다. 이 가설의 장점을 최대한 살리기 위해 
 HotSpot VM에서는 크게 2개의 물리적 공간을 나누었다. - Young area, Old area


    - Young Generation 영역 : <br>
        1. 새롭게 생성한 객체의 대부분이 여기에 위치. 
        2. 대부분의 객체가 금방 접근 불가능이 되기 때문에, 매우 많은 객체가 Young에 생성되었다가 
        사라진다. 이 영역에서 객체가 사라질 때, Minor GC가 발생한다고 말한다.
    - Old Generation 영역 : <br>
        1. 접근 불가능 상태가 되지 않아, Young 영역에서 살아남은 객체가 여기로 복사된다. 대부분 Young
        영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다. 이 영역에서 객체가 
        사라질 때, Major GC or Full GC가 발생한다고 말한다.
        2. Old 영역의 객체가 Young 영역의 객체 잠조할 때, 512 byte의 chunk(덩어리)로 되어 있는 
        카드 테이블(card table) 사용.
        3. card-table에는 Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때마다 정보가 표시.
        Young 영역의 GC 실행시, Old 영역에 있는 모든 객체의 참조를 확인하지 않고, 이 카드 테이블만 뒤져서
        GC 대상인지 식별한다.
        4. card-table은 write barrier를 사용하여 관리한다. write barrier는 Minor GC를 빠르게 할 수 있게
        하는 장치. write barrier때문에 약간의 Overhead는 발생하더라도, 전반적인 GC 시간은 줄어든다.
        
 ### Young 영역의 구성
     - GC를 이해하기 위해서 객체가 제일 먼저 생성되는 Young 영역에 대해 알아본다.
     - Young 영역의 3가지 영역
         1. Eden 영역
         2. Suvivor 영역(2개)
         
     - 각 영역의 처리 절차를 순서에 따라서 기술하자
         1. 새로 생성한 대부분의 객체는 Eden 영역에 위치.
         2. Eden 영역에서 GC가 한 번 발생한 후, 살아남은 객체는 Survivor 영역 중 하나로 이동.
         3. Eden 영역에서 GC가 발생하면, **이미 살아남은** 객체가 존재하는 Survivor 영역에 객체가 
         계속 쌓인다.
         4. 하나의 Survivor 영역이 가득 차게 되면, 그 중에서 살아남은 객체를 다른 Survivor 영역으로 
         이동한다. 그리고 가득찬 Survivor 영역은 아무 데이터도 없는 상태가 된다.
         5. 이 과정을 반복하다가 계속해서 살아남아 있는 객체는 Old 영역으로 이동하게 된다.
