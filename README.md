# 자바 정렬

### Comparable : 기본 정렬기준을 구현하는데 사용.
### Comparator : 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용.

### 1.배열기준 Array
Arrays.sort()는 String의 Comparable 구현에 의해 정렬된 것이다.

Comparable을 구현하고 있는 클래스들은 같은 타입의 인스턴스들끼리 서로 비교할 수 있는 클래스들이다. (String, Integer, Date, File)
기본적으로 작은값 -> 큰값 ,  오름차순 형태로 구현되도록 만들어져 있다.

### 2.리스트 형태 기준 ArrayList
Collections.sort()를 적용해야 한다.


```swift
import java.util.ArrayList;
import java.util.Collections;


class SoccerPlayer implements Comparable<SoccerPlayer>{ // Comparable 을 implements 한다.
	
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

