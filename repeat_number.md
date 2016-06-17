# N/3  Repeat NumberBookmark
---
You’re given a read only array of n integers. Find out if any integer occurs more than n/3 times in the array in linear time and constant additional space.

If so, return the integer. If not, return -1.

If there are multiple solutions, return any one.

---

## My Solution
```java 
public class Solution {
	// DO NOT MODIFY THE LIST
	public static int repeatedNumber(final List<Integer> a) {
	    ArrayList<Integer> a1 = new ArrayList<Integer>();
	    ArrayList<Integer> a2 = new ArrayList<Integer>();
	    int cnt1=0,cnt2=0;
	    if (a.size()==0) return -1;
	    if (a.size()<=2) return a.get(0);
	    for(int i=0;i<a.size();i++){
	        if(a1.isEmpty() && a2.isEmpty()){
	            a1.add(a.get(i));
	            cnt1++;
	        } else if(!a1.isEmpty() && a2.isEmpty()){
	            if (a.get(i).equals(a1.get(0))){
	                cnt1++;
	            } else {
	                a2.add(a.get(i));
	                cnt2++;
	            }
	        } else if(!a1.isEmpty() && !a2.isEmpty()){
	            if(a.get(i).equals(a1.get(0))) cnt1++;
	            else if(a.get(i).equals(a2.get(0))) cnt2++;
	            else{
	                cnt1--;
	                cnt2--;
	                if(cnt1 == 0) a1.remove(0);
	                if(cnt2 == 0) a2.remove(0);
	            }
	        } else{
	            if (a.get(i).equals(a2.get(0))){
	                cnt2++;
	            } else {
	                a1.add(a.get(i));
	                cnt1++;
	            }
	        }
	    }
	    if(a1.isEmpty() && a2.isEmpty()) return -1;
	    else if(!a1.isEmpty() && !a2.isEmpty()) {
	        cnt1=0;
	        cnt2=0;
	        for(int i=0;i<a.size();i++){
	            if(a.get(i).equals(a1.get(0))) cnt1++;
	            if(a.get(i).equals(a2.get(0))) cnt2++;
	        }
	        if(cnt1>a.size()/3) return a1.get(0);
	        else if(cnt2>a.size()/3) return a2.get(0);
	        else return -1;
	    }
	    else if(!a1.isEmpty()){
	        cnt1=0;
	        for(int i=0;i<a.size();i++){
	            if(a.get(i).equals(a1.get(0))) cnt1++;
	        }
	        if(cnt1>a.size()/3) return a1.get(0);
	        else return -1;
	    }else{
	        cnt2=0;
	        for(int i=0;i<a.size();i++){
	            if(a.get(i).equals(a2.get(0))) cnt2++;
	        }
	        if(cnt2>a.size()/3) return a2.get(0);
	        else return -1;
	    }
	}
}
```
