# 자바 정렬

## Comparable : 기본 정렬기준을 구현하는데 사용.
- 정의 : 정렬 수행시 기본적으로 적용되는 정렬 기준이 되는 메서드를 정의해 놓은 인터페이스
- 사용법 : Comparable 인터페이스를 implements한 뒤, 내부에 있는 compareTo메서드를 원하는 정렬 기준대로 구현
- 패키지 : java.lang.Comparable
- 자바에서 제공되는 정렬리 가능한 클래스들은 모두 Comparable인터페이스를 구현하고 있으며, 정렬시에 Comparable의 구현 내용에 맞춰 정렬 수행
   

## Comparator : 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용.
- 정의 : 정렬 가능한 클래스(Comparable이 구현된 클래스)들의 기본 정렬 기준과 다른 방식으로 정렬하고 싶을때 사용하는 클래스
- 사용법 : Comparator클래스를 생성하여, 내부에 compare메서드를 원하는 정렬 기준대로 구현 
- 패키지 : java.util.Comparator
- 주로 익명클래스(new Comparator(){...})로 사용됨


<hr/>

### 1.배열기준 Array
Arrays.sort()는 String의 Comparable 구현에 의해 정렬된 것이다.

Comparable을 구현하고 있는 클래스들은 같은 타입의 인스턴스들끼리 서로 비교할 수 있는 클래스들이다. (String, Integer, Date, File)
기본적으로 작은값 -> 큰값 ,  오름차순 형태로 구현되도록 만들어져 있다.

### 2.리스트 형태 기준 ArrayList
Collections.sort()를 적용해야 한다.


### Comparable을 이용한 정렬 
Comparable을 Implements한 뒤 compareTo 메소드를 구현하여 해결한다.

```swift
import java.util.ArrayList;
import java.util.Collections;


class SoccerPlayer implements Comparable<SoccerPlayer>{ // Comparable 을 implements 한다.
   //  SoccerPlayer 클래스들 끼리 비교하는 것이므로 제네릭스 타입도 SoccerPlayer가 된다.

   // 정렬 기준을 이름, 포지션, 나이로 잡는다.	
   private String name;
   private String position;
   private int age;
   
   public SoccerPlayer(String name, String position, int age) {
	   this.name = name;
	   this.position = position;
	   this.age = age;
   }
   
	public String getName() { return name; }

	public void setName(String name) { this.name = name; }

	public String getPosition() { return position; }

	public void setPosition(String position) { this.position = position; }

	public int getAge() { return age; }

	public void setAge(int age) { this.age = age; }


	@Override
	public int compareTo(SoccerPlayer player) { // compareTo를 오버라이드 한다. , 매개변수는 SoccerPlayer
		
		return name.compareTo(player.getName()); // 정렬 기준을 name
	}
	
}

public class Main  {
	
	public static void main(String[] args)  {
    	
	    ArrayList<SoccerPlayer> SPList = new ArrayList<SoccerPlayer>();
	    
	    SoccerPlayer sp1 = new SoccerPlayer("손흥민","SS",27);
	    SoccerPlayer sp2 = new SoccerPlayer("기성용","MF",30);
	    SoccerPlayer sp3 = new SoccerPlayer("차범근","FW",50);
	    
	    SPList.add(sp1);
	    SPList.add(sp2);
	    SPList.add(sp3);
	    
	    Collections.sort(SPList);
	    
	    for(int i = 0; i<SPList.size(); i++) {
	    	   System.out.println(SPList.get(i).getName() + "-"+SPList.get(i).getPosition() + "-"+SPList.get(i).getAge());
	    }
	    
	}	
	
}

```

```
[결과]
기성용-MF-30
손흥민-SS-27
차범근-FW-50

```

### Comparator를 이용한 정렬 

```swift
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;


class SoccerPlayer { 
	
   // 정렬 기준을 이름, 포지션, 나이로 잡는다.	
   private String name;
   private String position;
   private int age;
   
   public SoccerPlayer(String name, String position, int age) {
	   this.name = name;
	   this.position = position;
	   this.age = age;
   }
   
	public String getName() { return name; }

	public void setName(String name) { this.name = name; }

	public String getPosition() { return position; }

	public void setPosition(String position) { this.position = position; }

	public int getAge() { return age; }

	public void setAge(int age) { this.age = age; }
	
}

public class Main  {
	
	public static void main(String[] args)  {
    	
	    ArrayList<SoccerPlayer> SPList = new ArrayList<SoccerPlayer>();
	    
	    SoccerPlayer sp1 = new SoccerPlayer("손흥민","SS",27);
	    SoccerPlayer sp2 = new SoccerPlayer("기성용","MF",30);
	    SoccerPlayer sp3 = new SoccerPlayer("차범근","FW",50);
	    
	    SPList.add(sp1);
	    SPList.add(sp2);
	    SPList.add(sp3);
	    
	    // Comparator를 이용하여 정렬한다.
	    Collections.sort(SPList, new Comparator<SoccerPlayer>() { // Object의 특정 변수 기준으로 정렬시 

			@Override
			public int compare(SoccerPlayer player1, SoccerPlayer player2) {
			
				if(player1.getAge() > player2.getAge()) {
					return 1;
				}else if(player1.getAge() < player2.getAge()) {
					return -1;
				}else {
					return 0;	
				}
				
			}
	    	
	    });
	    
	    for(int i = 0; i<SPList.size(); i++) {
	    	   System.out.println(SPList.get(i).getName() + "-"+SPList.get(i).getPosition() + "-"+SPList.get(i).getAge());
	    }
	    
	}	

	
}

```

```
[결과]
손흥민-SS-27
기성용-MF-30
차범근-FW-50
```
