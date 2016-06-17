# N/3 Repeat Number
---
You’re given a read only array of n integers. Find out if any integer occurs more than n/3 times in the array in linear time and constant additional space.

If so, return the integer. If not, return -1.

If there are multiple solutions, return any one.

---
## Discussions
Assume that we maintain 2 elements with their counts as we traverse along the array.

When we encounter a new element, there are 3 cases possible :
- We don’t have 2 elements yet. So add this to the list with count as 1.
- This element is different from the existing 2 elements. As we said before, we have 3 distinct numbers now. Removing them does not change the answer. So decrement 1 from count of 2 existing elements. If their count falls to 0, obviously its not a part of 2 elements anymore.
- The new element is same as one of the 2 elements. Increment the count of that element.

Consequently, the answer will be one of the 2 elements left behind. If they are not the answer, then there is no element with count > N / 3.
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
