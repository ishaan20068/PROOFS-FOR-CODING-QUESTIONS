# Algorithm:

1. First check if the total gas that can be acquired
   is less than the the total cost that the car has to pay on the trip. if sum of elements of cost is greater than the sum of elements gas then return -1

2. let target=0 and value=0

3. for 1<=i<=n:
    if val+gas[i]-cost[i]<0:
        then set val=0 and set target=i+1
    else:
        val+=gas[i]-cost[i]

4. return target


## Lemma 1
#### if sum of all values in cost > sum of all values in gas then there will be no solution

#### Proof

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