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
$\displaystyle\sum_{i=0}^{n-1}{gas[i]}<\sum_{i=0}^{n-1}cost[i]$ if and only if there is no solution possible.

### __Proof__  
Let us say that this $\displaystyle\sum_{i=0}^{n-1}{gas[i]}<\sum_{i=0}^{n-1}cost[i]$. Assume that for any test case with this property there must be one element say element number $i$ in the array from $0$ to $n-1$ such that starting from this element takes us to the desired solution.  

So, now in the first step, we start by taking all the fuel __gas[i]__ and we spend fuel __cost[i]__ to move from $i$
to $i+1$.  
Now, if this is a valid solution then at all times the fuel in the fuel tank must be non negative. because negative fuel in going from one place to another would mean that the fuel was over in between the trip.
Now, in going from $j$ to $j+1$ we get __gas[j]__ amount of fuel and we spend fuel __cost[j]__ to move from $j$
to $j+1$.  
So, in the total round trip the cost of fuel incurred is $\displaystyle\sum_{i=0}^{n-1}\textbf{cost[i]}$ and the fuel gained during the way is $\displaystyle\sum_{i=0}^{n-1}\textbf{gas[i]}$. For, completion of the trip the fuel in the tank should never be negative. Now, at the end of the trip the fuel in the tank is $\displaystyle\sum_{i=0}^{n-1}\textbf{gas[i]-cost[i]}$.  
But, now because of our assumption we have: 

$\displaystyle\sum_{i=0}^{n-1}{gas[i]}<\sum_{i=0}^{n-1}cost[i]\Rightarrow \displaystyle\sum_{i=0}^{n-1}\textbf{gas[i]-cost[i]}<0 $  

So, finally the fuel in the tank is negative, which implies that our assumption of existence of a solution is incorrect. This proves the forward part.


Now, if we assume that a solution exists, then at the end the fuel in the tank must be non negative quantity. So, we must have $\displaystyle\sum_{i=0}^{n-1}{gas[i]}> \sum_{i=0}^{n-1}cost[i]$. This proves the backward implication by contraposition.









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