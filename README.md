# POJ1015_Jury Compromise
Dynamic programming,DP
In Frobnia, a far-away country, the verdicts in court trials are determined by a jury consisting of members of the general public.

First, several people are drawn randomly from the public. For each person in this pool, defence and prosecution assign a grade from 0 to 20 indicating their preference for this person. 0 means total dislike, 20 on the other hand means that this person is considered ideally suited for the jury. 

Based on the grades of the two parties, the judge selects the jury. In order to ensure a fair trial: given a pool of n potential jurors and two values di (the defence's value) and pi (the prosecution's value) for each potential juror i, you are to select a jury of m persons. If J is a subset of {1,..., n} with m elements, then D(J ) = sum(dk)  k belong to J and P(J) = sum(pk) k belong to J are the total values of this jury for defence and prosecution. For an optimal jury J , the value |D(J) - P(J)| must be minimal. If there are several jurys with minimal |D(J) - P(J)|, one which maximizes D(J) + P(J) should be selected. 


The input file contains several jury selection rounds. Each round starts with a line containing two integers n and m. n is the number of candidates and m the number of jury members. These values will satisfy 1<=n<=200, 1<=m<=20 and of course m<=n. The following n lines contain the two integers pi and di for i = 1,...,n. A blank line separates each round from the next. The file ends with a round that has n = m = 0. 

Output, for each round output a line containing the number of the jury selection round ('Jury #1', 'Jury #2', etc.). On the next line print the values D(J ) and P (J ) of your jury as shown below and on another line print the numbers of the m chosen candidates in ascending order. Output a blank before each individual candidate number. Output an empty line after each test case. 

In order to facilitate the narrative problem, in any of the options, the difference between the total score of the defense and the total score of the prosecution is referred to as "the difference between the defense" and the sum of the defense and the total score of the prosecution is called " The sum between the defense".

The difference between the total score of the defense of the ith candidate and the total score of the prosecution is recorded as V (i), and the sum of the defense's total score and the total score of the prosecution is recorded as S (i).

dp (j, k) takes j candidates to make it a difference between k in all schemes, the defense and the largest scheme (the scheme is called "scheme dp (j, k)") .

Moreover, we also stipulate that if we can not choose j individuals, so that the difference is k, then dp (j, k) value is -1, also known as program dp (j, k) is not feasible. The question is to ask m individuals, then, if all the possible values ​​for k, find all the dp (m, k) (-20 × m ≤ k ≤ 20 × m), then the jury program naturally It was easy to find.
    The crux of the problem is to establish a recurring relationship. What kind of conditions do you need to start in order to find dp (j, k)? Obviously, the scheme dp (j, k) is evolved by a feasible scheme dp (j-1, x) (-20 × m ≤ x ≤ 20 × m).
The necessary condition for the feasible scheme dp (j-1, x) to evolve into scheme dp (j, k) is that there exists a candidate i, i is not selected in scheme dp (j-1, x), and x + V (i) = k. In the case of dp (j-1, x) satisfying the necessary condition, the maximum value of dp (j-1, x) + S (i) is selected, then the scheme dp (j-1, x) On the candidate i, it evolved into the program dp (j, k).
This is the middle of the need to choose a program which people are recorded. May wish to program dp (j, k) in the last selected candidate number, recorded in the two-dimensional array element path [j] [k]. Then the number of the penultimate candidate of the scheme dp (j, k) is path [j-1] [k-V [path [j] [k]]]. Assuming the final calculation of the solution to the difference is k, then from the path [m] [k] starting, you can follow suit step by step back to find all the candidates selected.
Initial conditions, can only determine dp (0, 0) = 0, the other is -1. From this point of view, a step by step from the bottom of the recursion, we can find all feasible solutions dp (m, k) (-20 × m ≤ k ≤ 20 × m). When the actual problem solving, will use a two-dimensional array dp to store the value of dp (j, k). Moreover, since the value of the difference in the argument k can be negative, and the program can not be negative for the number of subscriptions, so the program may wish to add the value of the difference in the correction value fix = 400, so as not to subscript A negative number leads to an error.
Why is fix = 400? This is very obvious, m upper limit of 20 people, when the 20 people are 0, p are 20, there will be a poor control of -400. After correction, avoid the negative index problem, the interval of the overall translation, from [-400,400] mapped to [0,800].
At this time the initial condition is corrected to dp (0, fix) = 0, others are -1.
DP, from the mth line of dp (m, fix) began to search on both sides of the smallest | DP | can, the first is not dp [m] [k]! = - 1 position k is the smallest | DP | .
The last is to find the individual D and P, because D + P = dp (m, | D-P |), | D-P | known.
(D + P + | D - P |) / 2, P = (D + P - | D - P |) / 2
When calculating D and P, note the correction value fix
