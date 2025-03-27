See the file mciver2025.probabilistic datatypes.challenge program.jpg which is a screen grab from the lecture.

The challenge program (CP) takes an argument N, a natural greater than zero, and returns a natural c, 0 <= c < N, selected uniformly at random. 

The CP uses a random choice between two options and equal probability each, i.e. 0.5. the code is this, with annotations in braces. I have used (+) to indicate the random choice.

The CP is efficient in that the random choices which are made in order to get to a result 0 <= c < N are all effective, none are wasted.

The scripts in the bash and python folders implement the algorithm.

The pdf contains my notes on the algorithm, based on the technologies discussed in Kaminski's 2019 PhD thesis [1]

[1] [Kam19] Benjamin Lucien Kaminski. Erweiterte wp-Kalkule fur Proba-
bilistische Programme. en. PhD thesis. RWTH Aachen Univer-
sity, 2019, p. 2019. doi: 10.18154/RWTH-2019-01829. url: https:
/ / publications . rwth - aachen . de / record / 755408 / files /
755408.pdf
