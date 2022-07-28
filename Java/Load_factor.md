# Load factor란?
    
HashMap으로 예를 들어보겠습니다.

HashMap은 외부에서 볼 때 항상 같은 형태인 것 같지만, 내부적으로 보면 capacity(용량 → 버킷의 수)과 load factor 라는 변인을 가지고 동적으로 변화합니다.  
여기서 capacity는 용량, 즉 버킷의 수를 의미합니다. 그리고 load factor는 해시 테이블의 버킷이 얼마나 가득 찾는지 보여주는 수치를 말합니다.  
이 값을 설정하지 않을 경우 init capcity는 16, load factor는 0.75로 설정돼 있습니다.  

실제 HashMap.class를 확인해보면 다음과 같습니다.
```java
public class HashMap<K, V> extends AbstractMap<K, V> implements Map<K, V>, Cloneable, Serializable {
    private static final long serialVersionUID = 362498820763181265L;
    static final int DEFAULT_INITIAL_CAPACITY = 16;
    static final int MAXIMUM_CAPACITY = 1073741824;
    static final float DEFAULT_LOAD_FACTOR = 0.75F;
    static final int TREEIFY_THRESHOLD = 8;
    static final int UNTREEIFY_THRESHOLD = 6;
    static final int MIN_TREEIFY_CAPACITY = 64;
    transient Node<K, V>[] table;
    transient Set<Map.Entry<K, V>> entrySet;
    transient int size;
    transient int modCount;
    int threshold;
    final float loadFactor;
```

HashMap은 load factor가 임계치(75%) 에 다다르면 resize를 통해서 새로윤 배열을 만들어 copy하며 이때 resize로 buket의 수(capcity)를 2배 증가시킵니다. (16 → 32) (이는 HashMap의 Hash 충돌에 대해서도 유의미 합니다!)  
이 특징으로 인해 bucket을 처음부터 많이 만들어 메모리를 낭비할 필요가 없이 bucket 수를 적게 가지고 시작해도 서서히 늘릴 수 있습니다. (하지만 resize의 행위가 많아 지면 그 또한 메모리를 낭비. 그렇기 때문에 대략적인 사이즈를 예측하면 좋습니다.)