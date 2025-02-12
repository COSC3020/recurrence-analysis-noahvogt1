# Recurrence Analysis -- Mystery Function
I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.

I used the internet to help remember how to solve that summation. It just popped up how to do it in the google thing answer.

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

It recursivly calls mystery function 3 times dividing n by 3 for each of the times giving us $3T(n/3)$. Then the first loop runs 
$n^2$  times, the second loop runs n times, and the third loop runs $n^2$  times. This gives us a total of $n^5$ times. Therefor
the recurrence relation would be $T(n) = 1$  for $n \le 1$  and $T(n) = 3T(n/3) + n^5$  for $n > 1$.

Solution to the recurrence relation:

$T(n) = 3T(n/3) + n^5$

$T(n) = 3(3T(n/9) + n^5/3^5) + n^5$  $= 9T(n/9) + n^5/3^4 + n^5$

$T(n) = 3^iT(n/3^i) + \sum_{k=0}^i n^5/3^{4k}$

Using $i = log_3(n)$  as a substitution for i:

$T(n) = nT(1) + n^5 \sum_{k=0}^i 1/3^{4k}$

That sum is a simple geometric series that simplifies to $1/(1-1/3^4)$ which is $80/81$ which is a constant.

$T(n) = nT(1) + 80/81 * n^5$

We ignore the lower order terms

$T(n) \in O(n^5)$



