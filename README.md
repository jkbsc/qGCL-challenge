See the file mciver2025.probabilistic datatypes.challenge program.jpg which is a screen grab from the lecture.

The challenge program (CP) takes an argument N, a natural greater than zero, and returns a natural c, 0 <= c < N, selected uniformly at random. 

The CP uses a random choice between two options and equal probability each, i.e. 0.5. the code is this, with annotations in braces. I have used (+) to indicate the random choice.

The CP is efficient in that the random choices which are made in order to get to a result 0 <= c < N are all effective, none are wasted.  (assertion in the lecture, not clearly understood by me)

```
{1/N} # precondition
var c, v = 0, 1
while(V<N or c>=N){
    {Inv x [v < N or C >= N]}
    [] (v <= N) -> v = 2v
        c = 2c (+) c = 2c+1
    [] (v > N) -> v,c=v-N,c-N
    {Inv}
}
{ [c=i] } # Post condition for any 0 <= i < N
```
The two guarded commands inside the while loop above govern two different loop constructs.

So, we convert to nested loops, first using repeat for the outer loop.
(But note that the algorithm can also be converted to two coroutines, see the coroutine file.)

```bash
# nested loops, with repeat (but incomplete, see the next refinement for better):

{ 1/N } # precondition
var v=1
var c=0
repeat {
   ...
      while (v<N or c>=N){
         {Inv and (v<N or c >= N)}
         : (v <= N ) -> v = 2v; c=2c (+) c=2c+1

         {Inv}
         }
      : (v > N )  -> v = v - N ; c = c - N
      } until (v>=N and c < N)
{(c = i) for some 0<=i<N} # Postcondition
```
Now modify the initialisation so that the outer loop can be expressed as a while:

```bash
# Inv includes c<v and (N=1 or v<2N)

{ 1/N } # precondition
var v=N+1
var c=N
while (c >= N){
   {Inv1 and c >=N}
                          # need to show N=1 or v<2N
   v = v - N ; c = c - N  # don't need the guard, (v > N) ->, since v>c>=N

   while (v<N){
       {Inv2 and (v<N)}   #  don't need 'or (c >= N)', in part because it is false, since c<v and v<N
                          #  but mostly because it controls the outer while loop, not the inner loop
       v = 2v; c=2c (+) c=2c+1
       {Inv2}
       }
   {Inv1}
   }
```
The algorithm terminates when N is a power of 2, after one cycle of the outer loop.

From now on, we set N not a power of 2, unless explicitly included.

The state space is a vector of pairs, length l, representing (c, p_c) where p_c means the probability of arriving at c.

We should be able to show that l=v
```
state_space=V(:0<=i<l:(i,p_i))
```
Want all p_i to be the same.
```
A(i,j:0<=i,j<l:p_i=p_j)  # this is part of the invariant
```
Should be able to prove that sum(p_i) = k^m where m is the number of the outer loop, m=0 for the first cycle, m=1 for the second &c and k is a fraction determined by the proportion of states that lead to the case c>=N, i.e. (v-N)/v. We have 0<=c<v, so once we get to v>=N, c falls either in the range [0,N) or in the range [N,v).  For N a power of 2, v=N after the first run of the inner cycle and the range [N,v) is empty. For N not a power of 2, the proportion (v-N)/v of states will lead to a fresh cycle of the outer loop.

Within the inner loop, sum(p_i) = (v-N)/v

{(c = i) for some 0<=i<N and A(i,j:0<=i,j<N: P(c=i)=P(c=j))} # Postcondition

Need to show that Post follows from v>=N and N>c and Inv1 and Inv2

Want to show that the probablity of termination converges to 1/N with each outer cycle

Want to show that the state space is recursive or self-similar, i.e. fractal

Want to show that the probability of getting into the next recursive part is a fixed fraction and therefore that the probability of the recursive parts reduces exponentially with each recursive cycle.

