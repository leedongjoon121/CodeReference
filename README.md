# 자바 정렬

### Comparable : 기본 정렬기준을 구현하는데 사용.
### Comparator : 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용.

#### 배열기준 Array
Arrays.sort()는 String의 Comparable 구현에 의해 정렬된 것이다.

Comparable을 구현하고 있는 클래스들은 같은 타입의 인스턴스들끼리 서로 비교할 수 있는 클래스들이다. (String, Integer, Date, File)
기본적으로 작은값 -> 큰값 ,  오름차순 형태로 구현되도록 만들어져 있다.

#### 리스트 형태 기준 ArrayList
Collections.sort()를 적용해야 한다.


