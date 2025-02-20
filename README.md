

```bash
# convert to nested loops, first with repeat:

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


# convert to nested loops, then with while:
Inv includes c<v, N=1 or v<2N

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

state_space=V(:0<=i<l:(i,p_i))
A(i,j:0<=i,j<l:p_i=p_j)  # this is part of the invariant

{(c = i) for some 0<=i<N and A(i,j:0<=i,j<N: P(c=i)=P(c=j))} # Postcondition

# need to show post follows from v>=N and N>c and Inv1 and Inv2
# want to show that the probablity of termination converges to 1/N with each outer cycle
# want to show that the state space is recursive or self-similar, i.e. fractal
# want to show that the probability of getting into the next recursive part is a fixed fraction and therefore that the probability of the recursive parts reduces exponentially with each recursive cycle.
```

