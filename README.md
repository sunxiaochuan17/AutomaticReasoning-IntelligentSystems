Hitori Puzzle Solver
============

This Hitori Puzzle Solver is one of the projects that I developed for the Knowledge Representation and Automatic Reasoning course in the junior year of my undergrad in computer science at UDC (Spain). It transforms the Hitori puzzle into a set of CNF boolean clauses based on the rules of the game, calls a SAT solver and creates the solution.

			Input:							Solution:
			531973765						5  *  1  9  7  3  *  6  * 
			382397634						3  8  2  *  9  7  6  *  4 
			517826647						*  1  *  8  2  6  *  4  7 
			167535456						1  6  7  *  3  *  4  5  * 
			415681732						4  *  5  6  8  1  *  3  2 
			456512348						*  5  6  *  1  2  3  *  8 
			834756193						8  *  4  7  5  *  1  9  3 
			732154226						7  3  *  1  *  4  2  *  6 
			578349721						*  7  8  *  4  9  *  2  1 


## Hitori puzzle

Hitori is played with a grid of squares or cells, with each cell initially containing a number. The objective is to eliminate numbers by blacking out some of the squares until no row or column has more than one occurrence of a given number. Additionally, black cells cannot be adjacent, although they can be diagonal to one another. The remaining numbered cells must be all connected to each other (we ignored this last restriction as per the assignment requirements).


## Problem solving

We basically transform the problem into 3-SAT (well known NP-Complete problem) and then use a SAT solver called picosat to solve it.
- For the first condition (no same number in the same row or column), we add a clause with pairs of variables and then a 0. For example, if the first row of the puzzle matrix is:
```
355163 
```
We are going to add the following clauses to avoid the 3 and 5 repetitions:
```
1 6 0 
2 3 0 
```
- For the second condition (non adjacent black cells), if two blacks are adjacent, we add a clause to make one of them white. For instance in the previous example, we will have to add the following clause to avoid element 2 and 3 to be possitive at the same time:
```
-2 -3 0
```

After we do that for the whole matrix, we call the SAT solver and if it is satisfiable, we generate the solution and print the matrix.


## Tools and execution

The project was developed using the following technology:

- python
- picosat

In order to execute different puzzles, change this line and reference the desired file: f = open("9x9.txt").
To execute the software, just run
```python hitori.py```, having picosat in the path.

It works for puzzles greater than 9x9 as long as the numbers are separated by space.
It outputs a file with the cnf clauses (cnf.txt), another with picosat's output (output.txt) and another with the solved hitori puzzle(solution.txt)


## Contact

Contact [Daniel Ruiz Perez](mailto:druiz072@fiu.edu) for requests, bug reports and good jokes.


## License

The software in this repository is available under the GNU General Public License, version 3. See the [LICENSE](https://github.com/DaniRuizPerez/TheoryOfComputationImplementations/blob/master/LICENSE) file for more information.
