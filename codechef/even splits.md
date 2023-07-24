# **EVEN SPLITS**
## <u>__Problem:__</u>

You are given a binary string $S$ of length $N$. You can perform the following operation on it:
1. Pick any non-empty even-length subsequence of the string.
2. Suppose the subsequence has length $2k$. Then, move the first $k$ characters to the beginning of $S$ and the other $K$ to the end of $S$ (without changing their order).
What is the lexicographically smallest string that can be obtained after performing this operation several (possibly, zero) times?
<br>
<br>

## <u>__Example:__</u>
Let $S=01100101110$. Here are some moves you can make (the chosen subsequence is underlined):

01<u>1</u>001<u>0</u>1110 $\rightarrow $ <u>1</u>010101110<u>0</u>

01<u>10</u>01<u>01</u>110 $\rightarrow $ <u>10</u>0101110<u>01</u>
<br>
<br>

## <u>__Algorithm:__</u>
<br>
1. if $S=10$ then output $10$.

2. Otherwise sort the binary string and output it.

Note that whenever the string is $10$ then we can only choose this whole string for the operation and that does not change this string.
<br>
<br>

## <u>__Lemma__</u>
if $|S|>2$ and $S$ starts with a $0$ character then the lexograohically smallest string that can be formed is the sorted string.
<br>

### __Proof__  
Let $S=0s_1s_2\dots s_k$. Now, let $s_i=1$, then we can select the subsequence $0s_i$ and this $1$ will move to the end. 

Continuing the same procedure for all the $1$'s, we can make the sorted string which is lexographically smallest among all the strings with the same characters.
<br>
<br>


## <u>__Theorem__ </u>
For all $S$ such that $|S|>2$, we can reduce it to the sorted string by doing the given operation.
<br>

### __Proof__
If $S$ has all same characters then it is itself the lexographically smallest string possible.

let $S$ contain atleast one $0$ and $1$. Now, if there is a $0$ at the end then we can do the operation on the subsequence $11$ or $01$ for some $1$ in the string. This would take a $1$ at the end. Now, we can do the operation on the subsequence $01$ at the end of the string. and this would take the $0$ to the front.

Now, by previous lemma, we can obtain the sorted string by doing the given operation.


Also, note that for any string with a smaller length the string will not show any change on doing the given operation. So, all the smaller strings remain the same.
<br>
<br>


## <u>__Code__</u>

The code for this problem is as follows:
```
int n;cin>>n;
string x;cin>>x;
if(x=="10"){cout<<"10"<<endl;continue;}
sort(x.begin(),x.end());
cout<<x<<endl;
```