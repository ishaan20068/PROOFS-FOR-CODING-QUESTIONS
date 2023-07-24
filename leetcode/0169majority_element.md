# **134. Majority Element**

## <u>__Algorithm:__</u>
<br>


1. initialise $element=a[0]$ and $count=1$
2. Keep moving forward and if the next element is same as $element$ then update $count+=1$ otherwise decrease $count-=1$
3. If $count$ hits zero at some point then move to the next element say $a[i]$ and set $ element=a[i]$ and $ count=1$ and continue the same process
4. The element we have at last is the majority element if the majority element exists.
<br>
<br>


## <u>__Lemma__</u>
If $count$ becomes zero after $k$ elements of the array have been traversed, and if $x$ was the majority element in the full array, then $x$ is the majority element in the remaining array of size $n-k$
<br>

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
<br>
<br>


## <u>__Theorem__ </u>
The algorithm mentioned gives the correct solution whenever a solution exists.
<br>

### __Proof__
If target remains zero throughout the algorithm then that means starting from zero would give a correct solution.  
Consider that target is initially set to $i$ and let us say that it is changed to $j+1$ such that $j>i$ right after the value $i$. Now, we need to just prove that there does not exist any $t$ such that $j\geq t >i$ and starting from $t$ gives us a solution to the problem. Let us assume the contrary.  
Note that this would mean that $\displaystyle\sum_{u=t}^jgas[u]-cost[u]\geq 0$ as the gas obtained from $t$ to $i$ has to be non negative. But we know that  $\displaystyle\sum_{u=i}^jgas[u]-cost[u]<0$ because we have changed the target variable from $i$ to $j$. Now, $\displaystyle\sum_{u=i}^jgas[u]-cost[u]<0$ $\displaystyle\Rightarrow \sum_{u=i}^{t-1}gas[u]-cost[u]+$ $\displaystyle\sum_{u=t}^jgas[u]-cost[u]<0$.  
But $\displaystyle\sum_{u=t}^jgas[u]-cost[u]\geq 0$, so we must have $\displaystyle\sum_{u=i}^{t-1}gas[u]-cost[u]< 0$. But in this case the variable target should have been set to $t$ before being set as $j$, which is a contradiction. So, there is no value $t$ such that $j\geq t >i$ and starting from $t$ gives us a solution to the problem. Therefore, in the algorithm, target is never set to a value from where we cannot attain a solution. Hence the algorithm generates a solution to the problem.
<br>
<br>


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