# **134. Gas Station**

## <u>__Algorithm:__</u>
<br>


1. First check if the total gas that can be acquired
   is less than the the total cost that the car has to pay on the trip. if sum of elements of cost is greater than the sum of elements gas then return -1

2. let target=0 and value=0

3. ```
    for 1<=i<=n:
        if val+gas[i]-cost[i]<0:
            then set val=0 and set target=i+1
        else:
            val+=gas[i]-cost[i]

4. return target
<br>
<br>


## <u>__Lemma 1__</u>
### Sum of all values in cost > sum of all values in gas if and only if there is no solution

### __Proof__  
Let us say that this lemma is incorrect. So, for any test case with this property there must be one element say element number $i$ in the array from $0$ to $n-1$ such that starting from this element takes us to the desired solution.  

So, now in the first step, we start by taking all the fuel from 








## <u>__Code__</u>

The code for this problem is as follows:
```
class Solution {  
public:  
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {  
        int money=0,petrol=0;  
        for(int i=0;i<gas.size();i++){  
            petrol+=gas[i];money+=cost[i];  
        }  
        if(money>petrol){return -1;}  
        int target=0;int val=0;  
        for(int i=0;i<gas.size();i++){  
            if(val+gas[i]-cost[i]<0){  
                val=0;target=i+1;  
            }  
            else{val+=gas[i]-cost[i];}  
        }  
        return target;  
    }  
};  
```