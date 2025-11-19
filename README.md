## Context

See the file mciver2025.probabilistic datatypes.challenge program.jpg which is a screen grab from the lecture.

The challenge program (CP) takes an argument N, a natural greater than zero, and returns a natural c, 0 <= c < N, selected uniformly at random. 

The CP uses a random choice between two options and equal probability each, i.e. 0.5.

The CP is efficient in that the random choices which are made in order to get to a result 0 <= c < N are all effective, none are wasted.

## Contributions

The original algorithm has been converted from a single loop with two guarded commands into two nested loops. Correctness of this translation is informal.

The state space of the algorithm is a fractal when shown as a graph indicating the transitions between one state and the next.

The state space is closely associated with the expansion of 1/N as a repeating binary decimal and the repeat is directly connected to the fractal state space. Further, the state space divides the probability distribution in an unusual way, not as N equal regions of the range \left[0,1\right] but as N fractal regions each of total size 1/N with each additional subsection corresponding to the increasingly accurate approximation of 1/N by its binary expansion.

We have shown an invariant for the two loops and we have shown conditional correctness, i.e. that the algorithm is correct in the case where it terminates.

It does not necessarily terminate when N is not a power of 2. However, in this case, the probability of non-termination decreases exponentially to zero.
The pdf contains my notes on the algorithm, based on the technologies discussed in Kaminski's 2019 PhD thesis [1]

## Implementation

The scripts in the bash and python folders are several separate implementations of the algorithm.

The python script 'nestedB' generalises the algorithm so that any integer 2 or greater can be used for the random selection. The
basic algorithm chooses uniformly at random between two options.  The generalisation chooses uniformly at random between B
options. B is for 'base': the basic algorithm is related to the representation of 1/N in base 2; the generalisation is related to
1/N represented in base B.

## References

[1] [Kam19] Benjamin Lucien Kaminski. Erweiterte wp-Kalkule fur Probabilistische Programme. en. PhD thesis. RWTH Aachen
University, 2019, p. 2019. doi: 10.18154/RWTH-2019-01829. url: https://publications.rwth-aachen.de/record/755408/files/755408.pdf
