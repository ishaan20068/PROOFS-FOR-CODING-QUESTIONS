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
If $count$ becomes zero for first time after $k$ elements of the array have been traversed, and if $x$ was the majority element in the full array, then $x$ is the majority element in the remaining array of size $n-k$
<br>

### __Proof__  
Let us say that the frequency of $x$ in the original array is $m$.
<br>
To the contrary assume that $x$ is not the majority element in the current array then we can have two cases:

#### __Case 1__ : the initial element was $x$
Because we have $count=0$, so the number of occurences of $x$ in the first $ k$ elements would have been $k/2$. as remaining $k/2$ elements would have brought the count to $0$ by decrementing.
<br>
<br>
Frequency of $x$ in the remaining subarray of size $ n-k = $ $m-k/2$.<br>
Now, as $x$ was a majority element, so $m>n/2\Rightarrow m-k/2>(n-k)/2$. So, the new frequency of $x$ is greater than half the size of the array. So, clearly $x$ is still the majority element in this case.
<br>
#### __Case 2__ : the initial element was $t \ (\neq x)$

Because we have $count=0$, so the number of occurences of $t$ in the first $ k$ elements would have been $k/2$. as remaining $k/2$ elements would have brought the count to $0$ by decrementing and $x$ would have occured in these remaining $k/2$ elements. So, if frequency of $x$ in the first $k$ elements is $l$, then $l\leq k/2$.
<br>
<br>
Frequency of $x$ in the remaining subarray of size $ n-k = $ $m-l$.<br>
Now, as $x$ was a majority element, so $m>n/2\Rightarrow m-l>n/2-l>n/2-k/2=(n-k)/2$. So, the new frequency of $x$ is greater than half the size of the array. So, clearly $x$ is still the majority element in this case too.
<br>
$\square$

<br>

## <u>__Theorem__ </u>
The final element we have is $x$ (the majority element)
<br>

### __Proof__
Note that after count goes $0$ for the first time, we have seen some elements. Now, according to the previous lemma the majority element among the remaining elements is still $x$. 
<br>
Now, the size of the remaining array goes decreasing. Now, if the final element is not $x$, then this means that all the occurences of $x$ would have been used in decrementing the frequency of the final element. But this is a contradiction as then the frequency of $x$ from the time $count$ was $0$ would not be resulting in majority.
<br>
<br>

## <u>__Code__</u>

The code for this problem is as follows:
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count=1;int element=nums[0];
        for(int i=1;i<nums.size();i++){
            if(count==0){count=1;element=nums[i];}
            else if(nums[i]!=element){count--;}
            else{count++;}
        }
        return element;
    }
};
```