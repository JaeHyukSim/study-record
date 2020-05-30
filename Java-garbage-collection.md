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
         6. HotSpot VM에서는 보다 빠른 메모리 할당을 위해서 두 가지 기술을 사용한다. 하나는 bump-
         the-pointer라는 기술, 다른 하나는 TLABs(Thread-Local Allocation Buffers)라는 기술.
         
### bump-the-pointer
    1. Eden 영역에 할당된 마지막 객체를 추적.(Eden 영역의 맨 위(top)에 존재)
    2. 다음에 생성되는 객체가 있으면, 해당 객체의 크기가 Eden 영역에 넣기 적당한지만 확인.
    3. 적당하다면 Eden - 매우 빠르게 메모리 할당이 가능
    4. **그러나** 멀티 쓰레드 환경을 고려하면 이야기가 달라진다. Thread-Safe를 하기 위해서 
    만약 여러 쓰레드에서 사용하는 객체를 Eden 영역에 저장하려면, lock이 발생, lock-contention 때문에
    성능은 매우 떨어진다. HotSpot VM에서 이를 해결한 것이 **TLABs** 이다.
    
### TLABs
    1. 각각의 스레드가 Eden 영역의 작은 덩어리를 가진다!
    2. 각 쓰레드는 자신의 TLAB에만 접근이 가능하여, lock이 필요 없이 메모리 할당이 가능하다.
    
### Old 영역에 대한 GC

- Old 영역은 기본적으로 데이터가 가득 차면 GC를 싱행한다. GC 방식에 따라서 처리 절차가 달라진다.
- GC 방식은 JDK 7을 기준으로 5가지 방식이 있다.
    + Serial GC (운영 서버에서 절대 사용하면 안되는 방식)
    + Parallel GC
    + Parallel Old GC(Parallel Compacting GC)
    + Concurrent Mark & Sweep GC(이하 CMS)
    + G1(Garbage First) GC
- 운영 서버에서 Serial GC 방식을 쓰면 안되는 이유 : Serial GC는 데스크톱의 CPU가 하나만 있을때 사용하기
위해서 만든 방식이므로.
- Serial GC 방식을 사용하면, 애플리케이션의 성능이 많이 떨어진다.

### Serial GC(-XX:+UseSerialGC)
- Old 영역의 GC는 mark-sweep-compact라는 알고리즘을 사용.
- 이 알고리즘의 첫 단계 : Old 영역에 살아 있는 객체를 식별(Mark)하는 것.
- 그 다음은 Heap의 앞 부분부터 확인하여 살아 있는 것만 남긴다(Sweep)
- 마지막 단계는 각 객체들이 연속되게 쌓이도록, 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과, 객체가 없는 부분으로 나눈다(Compaction)
- **Serial GC는 적은 메모리와 CPU 코어 개수가 적을 때 적합하다.**

### Parallel GC(-XX:+UseParallelGC)
- 기본적인 알고리즘은 Serial GC와 같다
- GC를 처리하는 쓰레드가 여러 개! - Serial GC보다 빠르게 객체를 처리할 수 있다.
- 메모리가 충분하고, 코어의 개수가 많을 때 유리하다
- Throughput GC라고도 부른다.

### Parallel Old GC(-XX:UseParallelOldGC)
- JDK 5 update 6부터 제공한 GC 방식이다.
- Parallel GC와 비교하여 Old 영역의 GC 알고리즘만 다르다. - Mark-Summary-Compaction
- Summary 단계는 Sweep단계와 다르게, 앞에서 GC를 수행한 영역에 대해서 별도로 살아있는 객체를 식별
- 약간 더 복잡한 단계

### CMS GC(-XX:UseConcMarkSweepGC)
- Initial Mark 단계 : 클래스 로더에서 가장 가까운 객체 중 살아있는 객체만 찾음.
- Concurrent Mark 단계 : 방금 살아있다고 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인.
이때, **다른 스레드가 실행 중인 상테어 동시에 진행**
- Remark 단계 : Concurrent Mark 단계에서 추가되거나 참조가 끊긴 객체를 확인. 
- Concurrent Sweep 단계: 쓰레기를 정리하는 작업을 실행. - **역시 다른 스레드가 실행 중인 상태에서**
- stop-the-world 시간이 짧아서 Low Latency GC.
- 다른 GC 방식보다 메모리와 CPU를 더 많이 사용
- Compaction 단계가 기본적으로 제공되지 않는다. - 메모리가 조각조각!
- Compaction 작업이 자주 수행되면 사용에 불리

## G1 GC (Garbage First GC)
- Young, Old 영역에 대한 내용 잊기
- 바둑판
- 장기적으로 말도 많고 탈도 많은 CMS GC 방식을 대체하기 위해 만들어짐
- 어떠한 GC보다 빠르다.
- 더 검증되야 한다.
