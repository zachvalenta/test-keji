# TODO

## 参考

📚
* ✅ Bhargava grokking algorithms
* Dasgupta algorithms
* MacCormick nine algorithms
* Skiena manual https://www.algorist.com/
* Wengrow ds/algos

## current

## queue

* rf fs
* Wengrow https://www.amazon.com/gp/product/1680507222
* Conery chapters

review data structures
* array https://www.youtube.com/watch?v=QJNwK2uJyGs
* linked list https://www.youtube.com/watch?v=odW9FU8jPRQ
* stack https://www.youtube.com/watch?v=I5lq6sCuABE
* queue https://www.youtube.com/watch?v=mDCi1lXd9hc
* hash table https://www.youtube.com/watch?v=jalSiaIi8j4
* probabilistic https://www.youtube.com/watch?v=VjFS-_H10bw @ 15:00

data structures in Python 🗄 `python.md` collections
* https://realpython.com/python-data-structures/
* https://malisper.me/an-algorithm-for-passing-programming-interviews/ 
* https://www.30secondsofcode.org/python/p/1

interviews
* reverse array in place w/ space compexity O(n) 🗄 `python.md` copy
* intersection of two lists https://jvns.ca/blog/2021/09/10/hashmaps-make-things-fast/
* recurring character https://crunchskills.com/most-common-interview-question-at-google
* previous interviews 🗄 `ms; rg def`
```python
start = 0
end = -1
terminus = len(qd) // 2
for _ in range(terminus):
    qd[start], qd[end] = qd[end], qd[start]
    start += 1
    end -= 1
return qd
```
```python
###
# PROBLEM STATEMENT
###
# Write a function that given a dictionary of key-values of stage-names to
# configurations (in this problem, stage names to integer timeout values) 
# and a stage name, will return the configuration value.

# EXAMPLE DATA
# typing: K (key) V (str/int)
configs = {
    "dev" : 3,
    "staging" : "prod",
    "UAT": 7,
    # "prod" : "default",
    "prod" : "staging",
    "default" : 42,
}

# ✅ step 1: handle K w/ int V
# ✅ step 2: handle K w/ str V i.e. transitive lookups
# step 3: handle non-existant K

def get_config_value(configs, env):
    count = 0
    """
    configs: data_src
    env: env
    >>> int
    """
    def get_config_value_inner(configs, env):
        if type(configs[env]) is int:
            return configs[env]
        else:
            if counter(count) == upper_limit:
                pass
                # bail out
            else:
                return get_config_value_inner(configs, configs[env])


# test case 1 - naive lookup
print(get_config_value(configs, "dev"))
print(get_config_value(configs, "UAT"))
print(get_config_value(configs, "default"))

# test case 2 - transitive lookup
print(get_config_value(configs, "staging"))
print(get_config_value(configs, "prod"))

# test case 3 - n transitive lookups
```
* `interview-cake` 
* https://www.hackerrank.com/interview/interview-preparation-kit
* 10 from Rosetta Code https://rosettacode.org/wiki/Category:Programming_Tasks https://www.freecodecamp.org/learn/coding-interview-prep/
* 10 from Euler https://www.freecodecamp.org/learn/coding-interview-prep/ https://projecteuler.net/archives
* https://interviewing.io/
* TripleByte

## done

* _21_: 📙 Trask chapters 1-3
* _20_: 📙 Bhargava grokking
* _19_: regex basics
* _18_: restart Bhargava
* _17_: start Bhargava, Castro and Roberto get everyone to buy the O'Reilly ML book
* _16_: Hacker Rank for Zip Code

# ALGORITHMS

🔍
* https://github.com/TheAlgorithms/Python
* https://softwareengineering.stackexchange.com/
> Until you start dealing with millions of people on a network or you need to blur or sharpen a million photos quickly, you can just use the work of other people. When it gets real, break out the comp sci. 🗄 `ford-code.pdf`

* _algorithm_: solution (Dijkstra) to specific problem (lightest path through unweighted graph)
* sometimes the name of the problem (set covering)

## classics

set covering
* given target set and a collection of source sets, find the smallest sub-collection of target sets whose union equals the target set
* howto (brute): go through power set, either O(2^n) or O(n!) 📙 Bhargava 8.147, 8.152, 9.162
```python

```
* howto (approximation): iterate source sets and take whichever has the most from the target set that hasn't been taken already, O(n^2) 📙 Bhargava 8.152
```python

```

knapsack problem https://en.wikipedia.org/wiki/Knapsack_problem
* given container w/ weight capacity (knapsack) and items w/ weights and values, calculate most valuable combination of items that could fit into container 📙 Bhargava 8.144, 9.162
* an example of combinatorics (part of stats? calculus? both? https://www.khanacademy.org/math/precalculus)
* ❓ version of set covering or different animal entirely?
* ❓ howto: last column serves as optimal solution until cell at last row and column, at which you compare previous optimal against...power set of all other other items? 📙 Bhargava 9.168  https://www.youtube.com/watch?v=YRBON9sIZ2Y https://aiven.io/blog/solving-the-knapsack-problem-in-postgresql

autocorrect
* _Levenshtein distance_: https://blog.paperspace.com/implementing-levenshtein-distance-word-autocomplete-autocorrect/ https://github.com/hbollon/go-edlib https://github.com/seatgeek/fuzzywuzzy https://www.youtube.com/watch?v=kTS2b6pGElE 🗄 `system.md` search https://towardsdatascience.com/text-similarity-w-levenshtein-distance-in-python-2f7478986e75
* people use DP?
* _substring_: common contiguous char [Bhargava 9.179, 182]
```markdown
y _bcd_ af 
x _bcd_ edf
```
* _subsequence_: discontiguous char; used for autocorrect [Bhargava 9.184]
```markdown
y _bcd_ a _f_
x _bcd_ ed _f_
```
* _substring_: char in order and continuous e.g. for `hello there` valid substrings are `hello` and `llo th` https://stackoverflow.com/a/49688118/6813490
* _subsequence_: char in order but not necessarily continuous e.g. for `hello there` a valid subsequences is `hll th` (note missing `e`)
> these moved in from different file, don't know which set of definitions valid

* _codec_: algo for video file compression https://github.com/leandromoreira/digital_video_introduction#how-does-a-video-codec-work https://news.ycombinator.com/item?id=25328622  https://github.com/ablwr/my-recurse-center-syllabus
* _Fibonacci_: 🗄 `classic-compsci.pdf` https://docs.python.org/3/tutorial/modules.html https://www.youtube.com/watch?v=anrOzOapJ2E @ 34:00 https://realpython.com/fibonacci-sequence-python/
* _Fisher-Jenks_: https://pbpython.com/natural-breaks.html
* _Huffman coding_: algo used to generate prefix code https://news.ycombinator.com/item?id=22474850
* _hyper log_: count unique items in large set 📙 Bhargava 11.213
* _Morris counter_: https://arpitbhayani.me/blogs/morris-counter
* _Prim's algorithm:_ find MST
* _PubGrub_: for dependency resolution (SAT) https://github.com/sdispater/mixology https://github.com/dart-lang/pub/blob/master/doc/solver.md
* _Towers of Hanoi_: 🗄 `classic-compsci.pdf` https://en.wikipedia.org/wiki/Dynamic_programming#Tower_of_Hanoi_puzzle

## search

🗄
* `math.md` linear algebra
* `systems.md` search engines

* _search space_: set of possible solutions to the problem constraints https://en.wikipedia.org/wiki/Feasible_region
* _simple_: 🗄 `/algos`
* _binary_: 🗄 `/algos`; using BST (❌ log O of n average case and O of n worst case, sequential access ✅ faster mutative operations) [Bhargava 11.205]
* _breadth-first (bfs)_: 🗄 `/algos` https://healeycodes.com/practical-intro-to-graphs/

---

* _A*_: https://www.redblobgames.com/pathfinding/a-star/introduction.html 
* _Bellman-Ford_: Dijkstra for negative-weighted [7.130]
* _dfs_: https://medium.com/basecs/deep-dive-through-a-graph-dfs-traversal-8177df5d0f13 
* _Dijkstra_: 🗄 `/algos` https://medium.com/basecs/finding-the-shortest-path-with-a-little-help-from-dijkstra-613149fbdc8e https://en.wikipedia.org/wiki/Dynamic_programming#Dijkstra's_algorithm_for_the_shortest_path_problem
* _optimal stopping_: related to dynamic programming, Bellman 📙 Christian chapter 1 https://en.wikipedia.org/wiki/Optimal_stopping
* _traveling salesperson(TSP)_: Bhargava 8.157 https://medium.com/basecs/the-trials-and-tribulations-of-the-traveling-salesman-56048d6709d seems like genetic algorithms are popular for this https://www.youtube.com/watch?v=9zfeTw-uFCw https://towardsdatascience.com/evolution-of-a-salesman-a-complete-genetic-algorithm-tutorial-for-python-6fe5d2b3ca35 https://www.quantamagazine.org/computer-scientists-break-traveling-salesperson-record-20201008/ https://news.ycombinator.com/item?id=24761105 📙 Christian chapter 8


## sort

🔗 https://xkcd.com/1185/
🗄 `python.md` sort
📙
* Christian ch. 3
* Conery ch. 8

quicksort https://en.wikipedia.org/wiki/Quicksort https://github.com/orlp/pdqsort
* strat: D&C via partition 📙 Bhargava 4.65 https://stackoverflow.com/q/164163
* time: O(n log n); iterate input multiple times but smaller input each time; parallel versions can be O(n) 📙 Bhargava 11.208 https://softwareengineering.stackexchange.com/a/297161
* space: O(n)

---

* _bubble_: https://realpython.com/sorting-algorithms-python/
* _heap_: 
* _insertion_: https://realpython.com/sorting-algorithms-python/
* _merge_: used for SSTables [Kleppmann 76] https://realpython.com/sorting-algorithms-python/
* _natural_: put like w/ like re: ints, strings https://github.com/SethMMorton/natsort
* _selection_: 🗄 `algos`
* _Timsort_: https://realpython.com/sorting-algorithms-python/
* _topological_: [Bhargava 6.112]

## strategies

🔗 https://en.wikipedia.org/wiki/Approximation_algorithm#Algorithm_design_techniques

---

* _dynamic programming (DP)_: maximize X given constraint on Y or calculate optimum involves large numbers 📙 Bhargava 9.163, 178
* only works for independent problems 📙 Bhargava 9.177
* used for Towers of Hanoi, Dikstra, longest substring/sequence, Fibonacci
* must have optimal substructure and overlapping sub-problems https://en.wikipedia.org/wiki/Dynamic_programming#Computer_programming
* clean up https://ngoldbaum.github.io/posts/dynamic-programming/ https://skerritt.blog/dynamic-programming/#why-is-dynamic-programming-called-dynamic-programmin https://trekhleb.dev/blog/2018/dynamic-programming-vs-divide-and-conquer/

* _divide and conquer (D&C)_: winnow to atomic case using recursion
* most (but not all) recursive algos use D&C e.g. quicksort https://stackoverflow.com/a/53796319

* _brute force_: enumerate all possible solutions
* _partition_: split list into two smaller sub-lists 🗄 `linux.md` split
* _pivot_: el used to partition
* _MapReduce_: map (apply func to each item in el) reduce (combine els) [Bhargava 11.209-10] parallel doesn't mean new runtime is old_runtime/cores bc have to load balance btw core and merge results [ibid 11.208] https://en.wikipedia.org/wiki/Parallel_algorithm 🗄 `language.md` concurrency
* _hill-climbing_: local maxima https://diff.substack.com/p/big-tech-sees-like-a-state 📙 Christian 195

* decision tree 📙 MacCormick chapter 6 https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/ https://victorzhou.com/blog/information-gain/ https://mlu-explain.github.io/
* random forest https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/ https://victorzhou.com/blog/intro-to-random-forests/ https://mlu-explain.github.io/
* gini impurity https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/ https://victorzhou.com/blog/gini-impurity/

yet to use personally
* _approximation_: aim for good enough when optimal solution too expensive/NP [Bhargava 8.147] take local maximum https://en.wikipedia.org/wiki/Approximation_algorithm
* _genetic_: select best candidates from random population https://danielmiessler.com/blog/genetic-algorithms-could-be-more-significant-than-machine-learning/ there's also something called 'genetic programming' whose relationship to genetic algorithms is unclear https://stackoverflow.com/a/3821746
* _greedy_: recursively choose local optimum e.g. counting change, lightest edge in MST; might not lead to global optimum but that can be ok w/ NP [Bhargava 8.144-5] https://www.interviewcake.com/concept/python3/greedy
* _linear programming_: maximize target given constraints 📙 Bhargava 11.218

# COMPLEXITY

🔗 https://en.wikipedia.org/wiki/Computational_complexity https://en.wikipedia.org/wiki/Computational_complexity_theory

Big O
* worst-case asymptotic time complexity
* measured using base-2 logarithms 📙 Bhargava 1.7, 1.15 https://www.interviewcake.com/article/big-o-notation-time-and-space-complexity
* _asymptotic_: concerned w/ rate of growth vs. walltime 📙 Bhargava 1.12
* walltime affected by hw, compiler, input, what else is running on box

---

Conery ch. 6
> how to know when to consider average time vs. worst-case? 📙 Bhargava 11.205
* _hardware lottery_: what algos win depend on what hardware is available https://arxiv.org/abs/2009.06489
* Conery chapter 2
* https://www.youtube.com/watch?v=YX40hbAHx3s
* https://medium.com/age-of-awareness/a-brief-history-of-systems-science-chaos-and-complexity-d9198b1a198d
* https://www.kanopy.com/product/lo-and-behold-reveries-connected-world-0
* _entanglement_: everything is super complex now https://aeon.co/essays/is-technology-making-the-world-indecipherable everything has always been super complex https://www.edge.org/response-detail/26191
* https://how.complexsystems.fail/

* _time complexity_: growth rate re: number of executions https://www.interviewcake.com/article/python3/big-o-notation-time-and-space-complexity
* in Python https://wiki.python.org/moin/TimeComplexity
* multiple time complexities resolve to dominant complexity e.g. quicksort is O(n log n) https://softwareengineering.stackexchange.com/q/258509
* _space complexity_: growth rate re: memory usage https://www.interviewcake.com/article/python3/big-o-notation-time-and-space-complexity

## constants

* matter less than runtime esp. as input becomes arbitrarily large e.g. O(1) will dust O(n) if n is 1M even if O(1) is actually O(1 + 42) [4.72, IC]
* but still matter sometimes e.g quicksort is faster than merge sort [Bhargava 4.72] does yield some perf improvement https://danluu.com/algorithms-interviews/ e.g. improvement to constant that makes script 4 hours faster doesn't change Big O but does save you 4 hours https://www.interviewcake.com/article/python3/big-o-notation-time-and-space-complexity
```python
# DROP CONSTANTS
def all_plus_one(items):  # O(1 + n) = O(n)
    print(items[0])
    for item in items:
        print(item)

def half(items):  # O(n/2) = O(n)
    current_index = 0
    middle_index = len(items) / 2
    while start_index < middle_index:
        print(items[current_index])
        current_index += 1

def twice(items):  # O(2n) = O(n)
    for item in items:
        print(item)

    for item in items:
        print(item)

# DROP LESS SIGNIFICANT TERMS
def linear_and_quadratic():  # O(n + n^2) = O(n^2)
    for item in items:  # O(n)
        print(item)

    for i in items:  # O(n^2)
        for j in items:
            print(i, j)
```

## NP

* _NP_: non-deterministic polynomial time i.e. might get different solution each time (unlike most algos) and solutions will be in polynomial time
* used for decision problems
* how to solve https://news.ycombinator.com/item?id=28845593
* _decision problem_: problem w/ yes or no answer
* _NP-hard_: problems that are pretty goddamn hard
* _NP-complete_: not possible to solve quickly w/out approximation e.g. set covering [Bhargava 8.157, 159] 🗄 `system.md` SAT https://blog.robertelder.org/computer-science-for-engineers/
* _N = NP_: 不明觉厉 https://stackoverflow.com/a/1857342/6813490

## runtimes

🔗 https://stackoverflow.com/a/11611770

```yaml
# replace this with a generated graphs per runtime ++ graph for all together
/*** ===================================================================== ***\
 *           a         b    O(N^2)                      d                    *
 *     O(N!) a        b                O(N log N)    d                    c  *
 *           a      b                            d                 c         *
 *          a      b                          d             c        O(N)    *
 *          a    b                         d         c                       *
 *          a  b                       d      c                              *
 *         a  b                     d  c                                     *
 *         ab                   c                          O(1)              *
 *  e    e    e    e    ec   d    e    e    e    e    e     e    e    e      *
 *      ba        c      d                                                   *
 *    ba   c        d                       f    f    f    f    f    f    f  *
 ** cadf    f d    f    f    f    f    f       O(log N)                     **
\*** ===================================================================== ***/
```

✅ O(1)
* time: constant
* ops/100: 1
* map (if 1 K to V)
```python
def get_db_port():
    return DB_PORT
```

✅ O(log n)
* time: log
* ops/100: 6-ish 📙 Bhargava 1.15
* binary search, balanced BST 📙 Bhargava 11.205
```python
def binary(query, sorted_list):
    low_index = 0
    high_index = len(sorted_list) - 1
    while low_index <= high_index:
        mid = (high_index + low_index) // 2
        if sorted_list[mid] == query:  # assert midpoint
            return f"found {query}"
        elif sorted_list[mid] > query:  # rm high side
            high_index = mid - 1
        else:  # rm low side
            low_index = mid + 1
```

✅ O(n)
* time: linear
* ops/100: 100
* map (if n K to V)
```python
def get_db_port():
    return DB_PORT  # ❓ how does this work? wouldn't a successful lookup also then need to iterate?
```

✅ O(n log n)
* time: polynomial
* ops/100: 
* sorts
```python

```

✅ O(n^2)
* time: quadratic
* ops/100: 100k 
* traversing 2D array e.g. selection sort (❓ bubble, insertion)
* quadratic complexity 🗄 branching factor, power set https://www.natemeyvis.com/writing/on-quadratic-complexity/
```python
def selection_sort(unsorted_list):
    unsorted_list_len = len(unsorted_list)
    sorted_list = []
    for _ in range(unsorted_list_len):
        high = find_high_val(unsorted_list)
        sorted_list.append(high)
        unsorted_list.remove(high)
    return sorted_list
```

❌ O(2^n) 🗄 `math.md` power set
* time: exponential https://www.natemeyvis.com/writing/on-quadratic-complexity/
* set covering problem, knapsack problem
```python
def set_covering(states_needed, stations):
    states_covered = set()
    stations_chosen = list()
    while states_covered != states_needed:
        station_w_most_uncovered_states = None
        states_from_station_w_most = set()
        for station, states in stations.items():
            uncovered_from_current_station = states - states_covered
            if len(uncovered_from_current_station) > len(states_from_station_w_most):
                station_w_most_uncovered_states = station
                states_from_station_w_most = uncovered_from_current_station
        states_covered.update(states_from_station_w_most)
        stations_chosen.append(station_w_most_uncovered_states)
    return stations_chosen
```

✅ O(n!)
* time: factorial
* ops/100: more than billions
* traveling salesman
```python

```

# DATA STRUCTURES

🔗 https://www.interviewcake.com/data-structures-reference
🗄 `math.md` information design
📙 Conery ch. 7

probabilistic
* _probabilistic data structures_: CAP theorem but w/ accuracy, functionality, efficiency https://www.youtube.com/watch?v=VjFS-_H10bw 9:15
* _hyperloglog_: distinct el in set https://www.youtube.com/watch?v=VjFS-_H10bw 10:00 https://redis.com/redis-best-practices/counting/hyperloglog/

linked list https://realpython.com/linked-lists-python/ https://news.ycombinator.com/item?id=26620598
* singly or doubly linked https://lwn.net/Articles/827180/
* _memory_: discontiguous locations = sequential access [2.30]
* _O(1)_: write [Bhargava 2.28] delete [ibid]
* _O(n)_: read [Bhargava 2.28]
> seems like mutative operations only O(1) if items tracked and if everything not the first/last index is untracked then shouldn't it be O(n)? [Bhargava 2.30]
* _piece table_: append-only list used for editing text https://darrenburns.net/posts/piece-table/ 
* diff than rope? https://github.com/cessen/ropey https://github.com/prompt-toolkit/pyvim https://web.eecs.utk.edu/~azh/blog/challengingprojects.html

## ADT

ADT vs. data structure
* _abstract data type (ADT)_: interface https://stackoverflow.com/a/1692961 https://en.wikipedia.org/wiki/Abstract_data_type#Examples
* _data structure_: impl https://en.wikipedia.org/wiki/Data_structure https://realpython.com/python-heapq-module/#what-are-heaps
* everything is an ADT e.g. arrays in C stored contiguously in mem but are still types i.e. objects https://stackoverflow.com/questions/50450578/how-are-arrays-implemented-in-c
> when students learn data structures they (1) learn how they work theoretically (2) use off-the-shelf data structures to solve problems and (3) sometimes implement these data structures from scratch. However, I don’t often see classes exploring the off-the-shelf implementations https://akshayr.me/blog/articles/python-dictionaries
* https://github.com/jamiebuilds/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js https://www.youtube.com/watch?v=5cU1ILGy6dM http://paulmouzas.github.io/2014/12/31/implementing-a-hash-table.html
* http://infolab.stanford.edu/~ullman/focs.html
* IC bottom up https://www.interviewcake.com/article/python3/data-structures-coding-interview @ RAM https://drewdevault.com/2016/05/28/Understanding-pointers.html
* stack https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-stacks 
* queue https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-queues
* linked list https://medium.com/outco/reversing-a-linked-list-easy-as-1-2-3-560fbffe2088 https://www.youtube.com/watch?v=FSsriWQ0qYE https://realpython.com/courses/working-linked-lists-python/
* hash table https://news.ycombinator.com/item?id=24232752 https://thepythoncorner.com/dev/hash-tables-understanding-dictionaries/ https://www.youtube.com/watch?v=2Ti5yvumFTU
* array https://medium.com/@bsurajbh/implementing-arrays-with-python-7586206f0b13

operations https://github.com/jamiebuilds/itsy-bitsy-data-structures https://www.interviewcake.com/concept/python3/array
* _lookup_: read
* _insert_: add anywhere
* _delete_: rm anywhere
* _unshift_: add to start
* _push_: add to end
* _shift_: rm from start
* _pop_: rm from end

## array

ADT/DS
* _ADT_: el in sequence w/ random access, supports all operations 📙 Bhargava 2.30 https://www.interviewcake.com/concept/python3/array
* _impl_: contiguous memory locations

complexity
* _O(1)_: lookup [Bhargava 2.28] push/pop [ibid 5.90]
* _O(n)_: insert (esp. unshift) delete [Bhargava 2.28] slice https://www.interviewcake.com/concept/python3/slice

types
* _one-dimensional (1d)_: `[42, 3, 7]`
* _n-dimensional (nd)_: `[[42, 3, 7], [4, 13]]`

za
* _static array_: manual memory
* _dynamic array_: memory managed; autoresize on backing store overflow (create new larger array, cp over existing); Java `ArrayList` Python `list`; same Big O as array except pushes that require resizing, which are O(n) https://www.interviewcake.com/concept/python3/dynamic-array
* _backing store_: free space in dynamic array https://danluu.com/algorithms-interviews/
* _array slice_: use array subset to form new array; example of out-of-place 🗄 `language.md` memory/stack; O(n) in both time and space https://www.interviewcake.com/concept/python3/slice

## graph

🛠 https://github.com/networkx/networkx
📙 Kun ch. 6 https://en.wikipedia.org/wiki/Graph_theory

semantics
* _graph_: nodes + edges
* _node_: obj in graph
* aka vertex, point📙 Bhargava 6.99 
* _edge_: conection btw obj
* aka line, branch (in a tree)
* _root_: starting or topmost node in graph/tree
* _path_: series of edges from root to particular node
* _neighbors_: directly adjacent nodes 📙 Bhargava 6.99
* _undirected_: edges go both directions
* aka cyclic 📙 Bhargava 6.106
* _directed_: edge go one direction
* aka acyclic 📙 Bhargava 7.122
* _knowledge graph_: https://news.ycombinator.com/item?id=27245696
* category theory https://news.ycombinator.com/item?id=28953155
* doesn't add much value irl https://markusstrasser.org/p/bcd8bded-7136-4bb4-8f97-e8a3a7b6d926/
* graph of blogs https://astralcodexten.substack.com/p/links-for-april-644
* dependency graphs, build systems https://rhodesmill.org/brandon/slides/2021-06-colombia-remote/
* _cycle_: https://endcrawl.com/credits-ordering/
```python
# UNWEIGHTED
friends['me'] = {}  # root
network['me']['jack'] = 'jack kredell'  # children
network['me']['will'] = 'will bartlett'
network['me']['jack']['neil'] = 'neil ellner'  # grandchildren

# WEIGHTED 📙 Bhargava 7.120
network['root'] = {}
network['root']['amber'] = 5
network['root']['jack'] = 2
network['root']['sean'] = 6
```

## map

🗄 `system.md` search engines

* ADT: reference array via key https://calpaterson.com/how-a-sql-database-works.html
* impl: BST, red-black https://jvns.ca/blog/2017/09/09/data-structure--the-treap-/ hash table https://calpaterson.com/how-a-sql-database-works.html 📙 Kleppmann 72

hash tables 🗄 `security.md`
* _hash table_: hash function + array to put the results in [Bhargava 5.76-8, 5.90-2, 11.213]
* hashing https://blog.codinghorror.com/url-shortening-hashes-in-practice/
* aka map, dictionary
* alternatives incl. BST, skip list https://stackoverflow.com/a/301822 📙 Skiena 12.1

bloom filter
* _bloom filter_: like a hash table except takes up a lot less space and false positives are possible
* use case is to see whether item already part of a very large set e.g. whether a key exists in a database 📙 11.210-11
* https://vprusso.github.io/blog/2017/bloom-filters-and-pokemon/ 📙 Kleppmann 79 https://onatm.dev/2020/08/10/let-s-implement-a-bloom-filter/ http://aosabook.org/en/posa/working-with-big-data-in-bioinformatics.html

https://tenthousandmeters.com/blog/python-behind-the-scenes-10-how-python-dictionaries-work/
* _operations_: lookup, insert, delete
* _O(1)_: Bhargava 5.90
* _hash aggregate_: aggregate keys e.g. A 1 B 2 A 4 -> A 5 B 2 https://veekaybee.github.io/2021/06/06/hashaggregate/

## tree

🛠 https://github.com/joowani/binarytree
🔗 https://en.wikipedia.org/wiki/Phylogenetic_tree
> trees are easy to deal with and understand, but graphs are more "open" with what you can do https://news.ycombinator.com/item?id=27662089

semantics
* _tree_: type of graph 📙 Bhargava 6.113
* _parent_: node w/ children
* _leaf_: node with no children https://www.youtube.com/watch?v=5cU1ILGy6dM @ 0:30
* _height_: distance from root to leaf https://www.youtube.com/watch?v=Aagf3RyK3Lw @ 0:15
* measured in levels https://www.youtube.com/watch?v=dM_JHpfFITs @ 1:10
* _subtree_: tree nested w/ root tree https://www.youtube.com/watch?v=5cU1ILGy6dM
* _completeness_: know how many elements in each layer except the last one https://realpython.com/python-heapq-module/#heaps-as-lists-in-the-python-heapq-module

types
* _b-tree_: two branches for each node https://stackoverflow.com/a/6380314 🗄 `db.md` indexing  https://avi.im/blag/
* balanced = min height and max height differ by 1 (at most) https://www.youtube.com/watch?v=Aagf3RyK3Lw @ 0:50
```sh
  1
 / \
2   3
```
* _binary search tree (BST)_: left child only contains values less than parent and vice versa for right child 
* no random access but Big O average-case for search good as binary search + faster writes 📙 Bhargava 11.205
```sh
  2
 / \
1   3

     david
    /     \
adit       manning
          /       \
      maggie      mike
```
* _treap_: BST + each node has value + priority https://jvns.ca/blog/2017/09/09/data-structure--the-treap-/
* _heap_: tree + heap property e.g. max (parent node >= child nodes) min (parent node >= child nodes) https://www.youtube.com/watch?v=dM_JHpfFITs
* used for priority queue 🗄 *FO https://en.wikipedia.org/wiki/Heap_(data_structure)
```
    9
   / \
  5   7
 /     \
4       6
```
* _trie (prefix tree)_: typically used to store words https://www.youtube.com/watch?v=7XmS8McW_1U https://medium.com/basecs/trying-to-understand-tries-3ec6bede0014
* _BPS tree_: formed from binary space partitioning https://twobithistory.org/2019/11/06/doom-bsp.html
* _minimum spanning tree (MST)_: edges to connect every node in weight graph while minimizing edge weight 📙 Christian chapter 8
* _red-black tree_: BST that keeps itself balanced 📙 Bhargava 11.206
* used for SSTables 📙 Kleppmann 78
* _multitree_: https://github.com/climech/grit
* _splay tree_: red-black + recently accessed are fast to lookup again 📙 Bhargava 11.206

## *FO

* _dequeue_: *FO; either; push to each pop from each https://stackoverflow.com/a/38812944/6813490
```python
pass
```

* _stack_: LIFO; post-it https://stackabuse.com/stacks-and-queues-in-python/ https://realpython.com/how-to-implement-python-stack/
```python
stack = [42, 'abc']
stack.append('alice')  # push
stack.pop()  # pop
```

* _queue_: FIFO; line https://dbader.org/blog/queues-in-python + cf. 'rotate array' above
* _priority queue_: impl w/ heap https://realpython.com/python-heapq-module/
> is_empty checks whether the queue is empty. add_element adds an element to the queue. pop_element pops the element with the highest priority.
```python
queue = [42, 'abc']  # slow bc list is dynamic array https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-queues
queue.append('alice')  # push
queue.pop(0)  # shift

queue = deque([42, 'abc'])  # faster
queue.append('alice')  # push aka queue
queue.popleft()  # shift aka enque
```

# ML

🔍 https://ai.stackexchange.com/
🗄
* `algos.md` chess engine
* `math.md` algebra
📚
* Ferguson game of go
* Perrota programming ML https://www.amazon.com/Programming-Machine-Learning-Zero-Deep/dp/1680506609/ref=sr_1_1
* Trask grok deep learning https://github.com/iamtrask/Grokking-Deep-Learning

rf
* https://tigyog.app/d/C-I1weB9CpTH/r/everyday-data-science
* Ferguson section 1
* https://sirupsen.com/napkin/neural-net

za
* TigerGraph https://github.com/benedekrozemberczki/tigerlily
* _TinyML_: ML on devices e.g. phones, IoT https://www.thoughtworks.com/radar/techniques?blipid=202203070
* _computer vision_: ability of computer to process visual input; aka image recognition http://aiplaybook.a16z.com/docs/guides/vision
* _OCR_: map picture to text [Bhargava 10.199] aka image recognition https://news.ycombinator.com/item?id=26207049
* _VGA (visual question answering)_: answer open-ended question about image https://victorzhou.com/blog/easy-vqa/
* overlap btw stat and ML https://news.columbia.edu/news/top-10-ideas-statistics-ai
* multi-armed bandit, Gittins Index, upper confidence bound 📙 Christian chapter 2
* math: stat/probability, linear algebra https://nostarch.com/math-deep-learning

models
* _model_: machine impl algo (vs. human impl) https://github.com/minimaxir/automl-gs
* serialize https://onnx.ai/
* _gradient descent_: https://www.youtube.com/watch?v=IHZwWFHWa-w

libs
* _Tensorflow_: tensor (array) flow (operations) https://github.com/Hvass-Labs/TensorFlow-Tutorials
* _Keras_: less verbose Tensorflow (will eventually be packaged w/) https://victorzhou.com/blog/keras-neural-network-tutorial/
* _PyTorch_: superceded Tensorflow https://thegradient.pub/state-of-ml-frameworks-2019-pytorch-dominates-research-tensorflow-dominates-industry/ NumPy that can run in parallel on GPUs; tensor (array 类似 NumPy array) scalar (single value) vector (array) matrix (2d array) tensor (multi-dimensional array) https://aiweirdness.com/post/189170306297/how-to-begin-a-novel alternative https://github.com/geohot/tinygrad
* _CUDA_: GPUs aaS
* _sci-kit learn_: https://jakevdp.github.io/PythonDataScienceHandbook/
* _Matplotlib_: Matlab for Python https://jakevdp.github.io/PythonDataScienceHandbook/
* _Numpy_: subset of scipy https://jakevdp.github.io/PythonDataScienceHandbook/ 📙 Trask 44
```python
# numpy.array.dot https://stackoverflow.com/a/35208273 📙 Trask 3.35
def dot(v1, v2):  # vectors
    return sum(x*y for x,y in zip(v1,v2))

dot([1,2,3], [4,5,6])
```

operationalizing
* MLflow https://www.thoughtworks.com/radar/tools/mlflow metaflow https://www.thoughtworks.com/radar/tools?blipid=202203023
* can't debug like traditional programming [Ferguson 7] unexplainable? https://blog.cerebralab.com/Machine_learning_could_be_fundamentally_unexplainable
* aka ml ops https://news.ycombinator.com/item?id=20865012 https://testdriven.io/blog/machine-learning-reliability-engineering/
* web app integration https://github.com/xadrianzetx/fullstack.ai https://news.ycombinator.com/item?id=20865012 https://talkpython.fm/episodes/transcript/226/building-flask-apis-for-data-scientists https://testdriven.io/blog/fastapi-machine-learning/
* quants can't code, coders can't quant https://news.ycombinator.com/item?id=23941075
* 90% of the job is munging data, models are implemented by people w/ PhDs https://towardsdatascience.com/the-cold-start-problem-how-to-build-your-machine-learning-portfolio-6718b4ae83e9 https://spectrum.ieee.org/view-from-the-valley/artificial-intelligence/machine-learning/andrew-ng-xrays-the-ai-hype more on job market https://evjang.com/2022/04/25/rome.html
* https://www.youtube.com/watch?v=JLTYNPoK7nw https://www.youtube.com/watch?v=pvaIi0l1GME https://softwareengineeringdaily.com/2019/06/13/stripe-machine-learning-infrastructure-with-rob-story-and-kelley-rivoire/

## AI

overrated
* https://news.ycombinator.com/item?id=30764701
* stagnation https://softwareengineeringdaily.com/2021/06/04/machine-learning-the-great-stagnation-with-mark-saroufim/
* ML hasn't solved radiology https://news.ycombinator.com/item?id=27422610
* as oracle https://marginalrevolution.com/marginalrevolution/2022/06/are-we-entering-an-age-of-oracles.html
* ethics as red herring https://blog.cerebralab.com/AI_alarmism_and_the_misinformed_position
* you mostly just need SQL + regression http://aiplaybook.a16z.com/docs/guides/dl https://news.ycombinator.com/item?id=25775872 https://www.youtube.com/watch?v=qw5dBdTXLEs https://ai.google/research/pubs/pub43146 https://nullprogram.com/blog/2020/11/24/
* job market has collapse for data science, big data, ML https://news.ycombinator.com/item?id=24330326 https://news.ycombinator.com/item?id=25775740
* ML doesn't think, only answers, and therefore can be hacked
> In 2017, M.I.T.’s LabSix—a research group of undergraduate and graduate students—succeeded in altering the pixels of a photograph of a cat so that, although it looked like a cat to human eyes, Inception became 99.99-per-cent sure it had been given a photograph of guacamole. (There was, it calculated, a slim chance that the photograph showed broccoli, or mortar.) Inception, of course, can’t explain what features led it to conclude that a cat is a cat; as a result, there’s no easy way to predict how it might fail when presented with specially crafted or corrupted data. Such a system is likely to have unknown gaps in its accuracy that amount to vulnerabilities for a smart and determined attacker. - https://www.newyorker.com/tech/annals-of-technology/the-hidden-costs-of-automated-thinking
> Well, in the past, if a software engineer wanted to create a system to recognise something, they would write logical steps (‘rules’). To recognise a cat in a picture, you would write rules to find edges, fur, legs, eyes, pointed ears and so on, and bolt them all together and hope it worked. The trouble was that though this works in theory, in practice it’s rather like trying to make a mechanical horse - it’s theoretically possible, but the decree of complexity required is impractical. We can’t actually describe all of the logical steps we use to walk, or to recognise a cat. With machine learning, instead of writing rules, you give examples (lots of examples) to a statistical engine, and that engine generates a model that can tell the difference. You give it 100,000 pictures labelled ‘cat’ and 100,000 labelled ‘no cat’ and the machine works out the difference. ML replaces hand-written logical steps with automatically determined patterns in data, and works much better for a very broad class of question - https://www.ben-evans.com/benedictevans/2018/12/19/does-ai-make-strong-tech-companies-stronger
* need data specific to problem
> First, though you need a lot of data for machine learning, the data you use is very specific to the problem that you’re trying to solve. GE has lots of telemetry data from gas turbines, Google has lots of search data, and Amex has lots of credit card fraud data. You can’t use the turbine data as examples to spot fraudulent transactions, and you can’t use web searches to spot gas turbines that are about to fail. https://www.ben-evans.com/benedictevans/2018/12/19/does-ai-make-strong-tech-companies-stronger

ways of learning https://danielmiessler.com/blog/machine-learning-new-statistics/
* event-based: no model + datum
* stat: fixed model + data
* AI: fluid model + data [Ferguson 7] https://blog.cerebralab.com/Replacing_statistics_with_modern_predictive_models

types
* _GAI_: Hal9000
* aka strong 📙 Thiel 150
* PALM https://ai.googleblog.com/2022/04/pathways-language-model-palm-scaling-to.html https://news.ycombinator.com/item?id=30908941 https://blog.samaltman.com/dall-star-e-2 aka language models https://marginalrevolution.com/marginalrevolution/2022/04/monday-assorted-links-351.html https://stratechery.com/2022/dall-e-the-metaverse-and-zero-marginal-content https://twitter.com/nickcammarata/status/1511861061988892675 large language models https://www.nytimes.com/2022/04/15/magazine/ai-language.html https://astralcodexten.substack.com/p/mantic-monday-41822 https://www.assemblyai.com/blog/how-dall-e-2-actually-works/ https://github.com/lucidrains/DALLE2-pytorch pictures https://news.ycombinator.com/item?id=31967141 GPT-3 for code docs https://news.ycombinator.com/item?id=32036224 prompts https://deephaven.io/blog/2022/08/08/AI-generated-blog-thumbnails/ Midjourney https://alexanderwales.com/the-ai-art-apocalypse/ https://midjourney.gitbook.io/docs/ https://discord.com/channels/662267976984297473 Stable Diffusion https://news.ycombinator.com/item?id=32644176
* _AI_: superset of machine learning
* other subsets [Ferguson 6]
* used interchangely w/ deep learning [Ferguson 7]
* 1956: Dartmouth Summer Research Project, Geoffrey Hinton https://www.technologyreview.com/s/608911/is-ai-riding-a-one-trick-pony/ https://fermatslibrary.com/s/a-proposal-for-the-dartmouth-summer-research-project-on-artificial-intelligence
* 1960s: classical AI i.e. use normal coding techniques (control flow, data structure) http://aiplaybook.a16z.com/docs/guides/ai Eliza chatbot (me: "I like to code" Elize: "how do you feel about that?")
* 2010s: Google DeepMind, OpenAI, Future of Humanity Institute
* _ML_: superset of deep learning [Trask 2.10] https://pragprog.com/titles/pplearn/programming-machine-learning/ https://dafriedman97.github.io/mlbook/content/introduction.html https://course18.fast.ai/ml 🗄 techniques
* _deep learning_: subset of ML using neural networks [Trask 2.10] just stats and calculus https://news.ycombinator.com/item?id=24593529
* _cybernetic_: https://en.wikipedia.org/wiki/Johns_Hopkins_Beast

## data science

🔍 https://datascience.stackexchange.com/
🗄
* `db.md` data eng / business intelligence
* `math.md` stat

* _data science_: stats w/ higher salary https://thestatsgeek.com/2019/08/08/whats-the-difference-between-statistics-and-machine-learning/
* more about the data than the ML https://news.ycombinator.com/item?id=27290246
* steps: import, clean, model, operationalize https://www.kamwithk.com/machine-learning-field-guide
* most work is infra and cleaning data, not modeling https://news.ycombinator.com/item?id=22806434
* interviewing https://github.com/alexeygrigorev/data-science-interviews/blob/master/theory.md

datasets https://ourworldindata.org/
* general: https://www.wikidata.org/ https://datasetsearch.research.google.com/ https://www.kaggle.com/datasets https://datausa.io/ https://www.splitgraph.com/ 
* art https://news.ycombinator.com/item?id=28445761
* finance: https://github.com/ranaroussi/yfinance
* housing: https://www.zillow.com/research/data/
* literature: https://bookbrainz.org/ https://news.ycombinator.com/item?id=25607809 https://news.ycombinator.com/item?id=24884789 https://en.wikisource.org/ OpenLibrary https://news.ycombinator.com/item?id=1394077 Goodbooks http://fastml.com/goodbooks-10k-a-new-dataset-for-book-recommendations/ https://github.com/zygmuntz/goodbooks-10k http://www.jessamyn.com/barth/index.html
* music: https://musicbrainz.org/
* population: https://simplemaps.com/data
* scientific: https://news.ycombinator.com/item?id=27365755
* census https://www.ipums.org/

## neural networks

functions
```python
def af(arg, weight):
    activation = arg * weight
    return activation
```
* _activation function (AF)_: arg * weight = activation 📙 Trask 9.162 https://stats.stackexchange.com/a/307295
* _weight_: importance of arg 📙 Trask 3.23, 3.27
* _activation_: return of AF https://stats.stackexchange.com/a/307295 https://www.youtube.com/watch?v=aircAruvnKk 3:25 📙 Trask 3.46
* _weighted sum_: multiply input by weights and sum; aka dot product 📙 Trask 3.30

propagation
* _datapoint_: arg to network as a whole (vs. weight) 📙 Trask 3.22
* _shape_: types of datapoints 📙 Trask 3.23
* _propagate_: pass datapoint to network 📙 Trask 3.22 e.g. pass n pixels for computer vision neural network
* _forward propagation_: datapoints go straight through network 📙 Trask 3.46
* _back propagation_: figuring out which weight from previous layer contributed to increased error at higher layer and updating it 📙 Trask 6.119 https://www.youtube.com/watch?v=Ilg3gGewQ5U
* _prediction_: return of neural network 📙 Trask 3.25

vectors
* _scalar_: single value 📙 Trask [3.45] Bradshaw [62]
* _vector_: list 📙 Trask 3.31
* _matrix_: list of lists 📙 Trask 3.41 e.g. NumPy array, Pandas dataframe
* _elementwise operation_: perform same operation on two vectors of equal length 📙 Trask 3.31 i.e. zip

basics https://www.youtube.com/watch?v=aircAruvnKk
* _neural network_: graph (network) that mimics the brain (neural) https://victorzhou.com/blog/intro-to-neural-networks/
* in NN, just a var holding boolean value https://www.youtube.com/watch?v=aircAruvnKk 2:55
* akin to logic gate https://victorzhou.com/blog/intro-to-neural-networks/
* as non-leaky abstraction https://blog.cerebralab.com/Neural_networks_as_non-leaky_mathematical_abstraction

types
* _deep_: https://www.freecodecamp.org/learn/machine-learning-with-python/how-neural-networks-work/how-deep-neural-networks-work
* _recurrent_: https://www.freecodecamp.org/learn/machine-learning-with-python/how-neural-networks-work/recurrent-neural-networks-rnn-and-long-short-term-memory-lstm https://victorzhou.com/blog/intro-to-rnns/
* _convolutional_: https://www.freecodecamp.org/learn/machine-learning-with-python/how-neural-networks-work/how-convolutional-neural-networks-work https://victorzhou.com/blog/intro-to-cnns-part-1/ good for computer vision https://www.youtube.com/watch?v=aircAruvnKk 2:10

## NLP

🗄
* `literature.md` distant reading
* `psychology.md` reading
* `system.md` search engine

basics
* _NLP_: linguistics + CS
* rule system (noun phrase can be followed by noun, article, etc.) to construct parse tree
* use cases: speech synthesis http://aiplaybook.a16z.com/docs/guides/nlp speech to text https://www.fullstackpython.com/blog/transcribe-recordings-speech-text-assemblyai.html
* libraries: nltk, spaCy
* _sentiment analysis_: determine emotional content https://aeon.co/ideas/why-are-pop-songs-getting-sadder-than-they-used-to-be
* _word cloud_: https://dataanalysis.substack.com/p/generating-a-word-cloud-in-python?s=r
* clean up https://nostarch.com/NLPPython https://codewords.recurse.com/issues/seven/data-driven-literary-analysis https://www.fast.ai/2019/07/08/fastai-nlp/ https://speakerdeck.com/pycon2015/adam-palay-words-words-words-reading-shakespeare-with-python https://victorzhou.com/blog/better-profanity-detection-with-scikit-learn/

semantics
* _tokenize_: break into words or subsets of words
* _span_: section of text https://rajpurkar.github.io/SQuAD-explorer/ https://0x65.dev/blog/2019-12-05/a-new-search-engine.html#fn1
* _stemming_: rm pre/suffix; can also mean to include related results from search engine e.g. search 'fish', get back results for 'fishy', 'fishing' https://news.ycombinator.com/item?id=24051229
* _parts of speech_: tokenization but for syntax
* _stopword removal_: strip out non-semantic words (articles, &c.)
* _n-gram_: items (word, phraes) collected from text https://en.wikipedia.org/wiki/N-gram use case (find most commonly occuring words) https://news.ycombinator.com/item?id=24286844
* _disambiguation_: teach the machine context ('cool' indicates temperature and social prestige)

## techniques

learning types
* _supervised_: labeled data during training, unlabeled during predication [Trask 2.11]
* _unsupervised_: unlabeled data during training and prediction [Trask 13]
* _reinforcement_: no labels but algo can tell if it's getting hotter or colder http://aiplaybook.a16z.com/docs/guides/dl-learning#user-content-reinforcementlearning
* _parametric_: modeler derives parameters [Trask 2.14, 2.18]
* _nonparametric_: model derives parameters [Trask 2.14, 2.18]

Monte Carlo 🗄 `math.md` Markov chain
* aka simulation 📙 Konnikova bluff Zuckerman simons
* https://sirupsen.com/napkin/problem-16-simulation 
* https://www.erichgrunewald.com/posts/simulations-of-diversity-hiring/
* https://conversationswithtyler.com/episodes/annie-duke/
* _Monte Carlo tree search (MCTS)_: domain independent https://www.youtube.com/watch?v=Fbs4lnGLS8M @ 12:00
* tree: roots = next moves, branches = n order paths
* search: takes weights from neural net, traverse branches, report back
* _Monte Carlo_: 📙 Christian chapter 9 https://pbpython.com/monte-carlo.html https://news.ycombinator.com/item?id=27379310
* determine weights for MCTS
* weights = secret sauce https://github.com/leela-zero/leela-zero
* _minimax_: predecessor to MCTS https://www.youtube.com/watch?v=Fbs4lnGLS8M @ 1:15 used in chess 4:30 https://marginalrevolution.com/marginalrevolution/2021/05/maradona-plays-minimax.html

k-NN 🗄 `math.md` regression
* _k-nearest neighbors_: taxonomize based on proximate elements i.e. those that have similar attributes
* form of supervised learning
* used for recommendation system, regression, OCR 📙 Bhargava [186,195,196]
* https://philippmuens.com/k-nearest-neighbors-from-scratch/
* https://www.freecodecamp.org/learn/machine-learning-with-python/machine-learning-with-python-projects/book-recommendation-engine-using-knn
* https://news.ycombinator.com/item?id=26328958
* https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/
* 📙 MacCormick chapter 6

regression
* _linear regression_: use set of numerical X values (e.g. study time, price of crude oil) to predict numerical Y values (e.g. test score, price of gasoline)
* BYO https://www.youtube.com/watch?v=VmbA0pi2cRQ https://www.youtube.com/watch?v=KsVBBJRb9TE
* in Pandas, SQL https://hakibenita.com/sql-for-data-analysis#linear-regression
* uses k-NN 📙 Bhargava 10.196 🗄 `algos.md`
* 名 relationship
> the common narrative that it's a fairly simple regression with size, where small startups are fast and large companies are slow, I don't think that's necessarily the case at all, where Facebook is a good example of a company that's remarkable at executing quickly from a technology point of view https://www.stitcher.com/podcast/mathew-passy/invest-like-the-best/e/71161348 25:00
* 动 plot relationship btw
> People have regressed spending by countries, states, and districts on outcome metrics for a long time, and they pretty much universally show that there is no relationship between spending and success as defined in traditional terms. https://freddiedeboer.substack.com/p/is-the-conventional-wisdom-on-educational
* _logistic regression_: use set of numerical X values (e.g. email attr) to predict categorical Y value (e.g. spam or no?) https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/

# PROJECTS

* personalization engine https://news.ycombinator.com/item?id=30778100

## chess engine

🗄 ML/techniques/Monte Carlo

* https://marginalrevolution.com/marginalrevolution/2022/06/alphazero-ideas.html
* https://www.youtube.com/watch?v=mPY69BJmlbs https://www.youtube.com/watch?v=mhCOlhUBcqw
* _UCI_: interface for chess engines https://chess.resistant.tech/
* _bitboard_: data structure used in board games https://en.wikipedia.org/wiki/Bitboard 
* BYO https://healeycodes.com/building-my-own-chess-engine/ https://github.com/notnil/chess testing https://chess.stackexchange.com/questions/21991/reasonable-engines-to-test-against-not-stockfishtic
* impl https://stackoverflow.com/q/1148727/ https://github.com/thomasahle/sunfish https://stats.stackexchange.com/q/308777/248351 https://waters.me/trying-to-beat-chess-computers/ https://github.com/CYHSM/chess-surprise-analysis 🗄 `za/cs/ml/deep-learning-w/go.pdf` https://news.ycombinator.com/item?id=20027838 https://www.youtube.com/watch?v=pUyURF1Tqvg FEN/PGN https://www.chess.com/analysis
* tic tac toe https://robertheaton.com/2018/10/09/programming-projects-for-advanced-beginners-3-a/ https://www.freecodecamp.org/learn/machine-learning-with-python/machine-learning-with-python-projects/rock-paper-scissors game tree https://www.youtube.com/watch?v=Fbs4lnGLS8M @ 1:25 every possible game https://defmacro.substack.com/p/how-to-interview-engineers
* za https://news.ycombinator.com/item?id=28765183 https://leahneukirchen.org/blog/archive/2019/10/ken-thompson-s-unix-password.html https://www.andreykurenkov.com/writing/ai/a-brief-history-of-game-ai/

Alpha Go https://www.newyorker.com/science/elements/how-the-artificial-intelligence-program-alphazero-mastered-its-games
* _AlphaGo_: 2016
* Go-specific
* used hard-coded heuristics and learned from master players https://marginalrevolution.com/marginalrevolution/2017/12/the-age-of-the-centaur-is-over.html
* _Stockfish_: former best chess engine before being surpassed by AlphaZero
* https://www.quora.com/Is-StockFish-AI-level-5-really-1700-ELO
```txt
Level 0 = 1100 ELO rating
Level 1 = 1165 ELO rating
Level 2 = 1230 ELO rating
As you can see the strength is increasing by 65 ELO points for each level, so that;
Level 20 = 2570 ELO rating.
However, these are approximate values and its hard to say for sure.
Stockfish 10 at its top strength (without any level set) has a rating of about 3500 ELO, which would be strong enough to be beat the world champion in almost every game.
```
* _AlphaGo Zero_: 2017
* generalizes to any two-person zero-sum game of perfect information
* impl: neural net + MCTS, learned only from the rules
* OSS https://github.com/leela-zero/leela-zero https://github.com/LeelaChessZero/lc0
* _AlphaZero_: OSS AlphaGoZero https://github.com/suragnair/alpha-zero-general

## rec system

> the primary metric for suggesting content still seems to be "stuff other people are reading/watching/playing/listening" https://news.ycombinator.com/item?id=24471525
* just regression by another name? 📙 Bhargava 10.193-195
* need linear algebra? https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/ https://github.com/microsoft/recommenders
* https://github.com/maciejkula/spotlight https://github.com/zygmuntz/goodbooks-10k https://blog.crunchydata.com/blog/recommendation_engine_in_postgres_with_pandas_and_python http://blog.untrod.com/2016/06/simple-similar-products-recommendation-engine-in-python.html https://www.pythonpodcast.com/surprise-with-nicolas-hug-episode-135/ https://stackabuse.com/creating-a-simple-recommender-system-in-python-using-pandas/ https://realpython.com/build-recommendation-engine-collaborative-filtering/ https://github.com/kakao/buffalo https://2020.pygotham.tv/talks/the-album-discoverer-an-album-recommendation-system/ https://pudding.cool/2018/05/similarity/ http://guidetodatamining.com/ https://sirupsen.com/napkin/problem-12-recommendations

## search engine

🗄
* `ml.md` NLP
* `za/search-engine` (port data to query sandbox)

FTS 📙 Karwin ch 17
* _full text search (FTS)_: search all text https://en.wikipedia.org/wiki/Full-text_search
* via db (Postgres) or specialized server (elasticsearch) https://news.ycombinator.com/item?id=27973497
* BYO https://artem.krylysov.com/blog/2020/07/28/lets-build-a-full-text-search-engine/ https://bart.degoe.de/building-a-full-text-search-engine-150-lines-of-code/
* _meta search_: search metadata https://calpaterson.com/metadata.html

semantics
* _index_: subset of terms http://jsomers.net/blog/allusion
* usage in scholarship https://news.ycombinator.com/item?id=30407460
```txt
apple  - pg 3, 42
banana - pg 27, 113
```
* _inverted index_: map w/ K as topic and V as pages (whether book or web) 📙 MacCormick 12, Bhargava 11.207 🗄 `db.md` indexing
* ❓ different than index?
* _concordance_: all terms + snippet/full text from page https://www.opensourceshakespeare.org/concordance/
```txt
Wilt thou ever be a foul-mouthed and calumnious knave
Virtue itself scopes not calumnious strokes.
Theres none stands under more calumnious tongues
```
* _query_: what you're searching for
* _page_: where you're looking; aka document https://0x65.dev/blog/2019-12-05/a-new-search-engine.html
* _match_: page containing query 📙 MacCormick 11
* _lexical match_: exact e.g. query 'eggplant' only matches 'eggplant'https://github.blog/2018-09-18-towards-natural-language-semantic-code-search/ 
>  It was merely capable of answering queries that were an exact match to the queries we had in our query logs. Yes, that meant we didn’t have a "real" search-engine, but a glorified cache. https://0x65.dev/blog/2019-12-05/a-new-search-engine.html
* _semantic match_: smart e.g. query 'eggplant' matches 'eggplant' and 'aubergine' https://0x65.dev/blog/2019-12-05/a-new-search-engine.html
* anchor text from link tags a good way to get around document noise https://0x65.dev/blog/2019-12-05/a-new-search-engine.html#fn2
> Anchor text, curated by humans, serves as a mini summary of the content of a page. By building an inverted index based on it rather than the entire content, one can achieve a significantly smaller and more importantly, less noisy index.
```txt
# noisy documents
# query:	eggplant dishes

* document:	Popular Youtuber eggplant dishes out a severe attack against the whole music industry
* document:	I am not a fan of eggplant, but here are some zucchini dishes...
* document:	Did you know that eggplant dishes cannot be refrigerated?
```
* _relevance_: order matches 📙 MacCormick 11
* algos https://simonwillison.net/2020/Dec/19/dogsheep-beta/ 🗄 `algos.md` Levenshtein
* aka ranking, content match https://0x65.dev/blog/2019-12-06/building-a-search-engine-from-scratch.html
* _query logs_: map of query to URL clicked e.g. query 'boxing' URL 'espn.com/boxing' https://0x65.dev/blog/2019-12-05/a-new-search-engine.html
> Ranking is where it gets controversial. When you rank, you pick winners and losers. https://news.ycombinator.com/item?id=20286953
> The big problem with all the off-the-shelf search solutions (RDBMS full-text search, ES, Algolia) is that search ranking is a complicated and subtle problem, and frequently depends on signals that are not in the document itself. Google's big insight is that how other people talk about a website is more important than how the website talks about itself, and its ranking algorithm weights accordingly. https://news.ycombinator.com/item?id=27978505
* user feedback plays a part
> we would need real users to measure changes in search relevance in order to be competitive https://0x65.dev/blog/2019-12-06/building-a-search-engine-from-scratch.html

impl
* Google has appox 60B documents indexed https://0x65.dev/blog/2019-12-06/building-a-search-engine-from-scratch.html
* https://news.ycombinator.com/item?id=28558884 https://news.ycombinator.com/item?id=33051393
```text
# page 1
# the dog stood at the mat
# 1   2   3     4  5   6

# page 2
# the cat sat   at the mat
# 1   2   3     4  5   6

* the: 1, 2
* dog: 1
* stood: 1
* at: 1, 2
* mat: 1, 2
* cat: 2
* sat: 2
```
* _phrase query_: match on entire phrase vs. single words e.g. page must have 'Jesus Christ' and not just 'Jesus' and 'Christ"  📙 MacCormick 14
* _word location_: location of word on page
* enables phrase query 📙 MacCormick 15
* _near query_: match on entire phrase within given proximity e.g. 'Jesus Christ' where 'Jesus' within n words of 'Christ' 📙 MacCormick 17
* enables ranking 📙 MacCormick 18
```text
# e.g. query "cat sat" returns 2-2, 2-3

* the: 1-1, 1-5, 2-1, 2-5
* dog: 1-2
* stood: 1-3
* at: 1-4, 2-4
* mat: 1-6, 2-6
* cat: 2-2
* sat: 2-3
```

aaS
* _Algolia_: record (JSON obj) field (attr on obj) clients https://github.com/algolia/algoliasearch-client-javascript https://github.com/algolia/algoliasearch-client-python
* _Elasticsearch_: use in Postgres https://github.com/zombodb/zombodb
* _Lucene_: framework https://stackoverflow.com/questions/15704644/difference-between-solr-and-lucene
* _Meilisearch_: https://github.com/meilisearch/MeiliSearch https://news.ycombinator.com/item?id=22685831 https://github.com/valeriansaliou/sonic https://softwareengineeringdaily.com/2019/03/20/elasticsearch-at-scale-with-volkan-yazici/ https://github.com/typesense/typesense https://news.ycombinator.com/item?id=25414389 https://tech.marksblogg.com/meilisearch-full-text-search.html
* _RediSearch_: built on Redis https://oss.redislabs.com/redisearch/
* _Solr_: built on Lucene https://blog.codepen.io/2016/05/24/091-solr/
* _Typesense_: https://github.com/typesense/typesense https://xkcd-search.typesense.org/ https://www.thoughtworks.com/radar/tools?blipid=202203031
* _whoosh_: project is dead https://github.com/gyllstromk/Flask-WhooshAlchemy/issues/69 https://stackoverflow.com/a/53338666/6813490 
* _Zinc_: https://github.com/zinclabs/zinc

corporate
* _crawler_: recursively navigates pages via links e.g. GoogleBot, BingBot https://www.interviewcake.com/question/python3/compress-url-list https://0x65.dev/blog/2019-12-06/building-a-search-engine-from-scratch.html
> Crucially, I would not have it crawling the entire web from the outset. Instead, it should crawl a whitelist of domains, or “tier 1” domains. These would be the limited mainly to authoritative or high-quality sources for their respective specializations, and would be weighed upwards in search results. Pages that these sites link to would be crawled as well, and given tier 2 status, recursively up to an arbitrary N tiers. https://drewdevault.com/2020/11/17/Better-than-DuckDuckGo.html
> A significant portion of the web is cut off from you if your crawler is not famous. Google has a huge competitive advantage in this regard, a lot of site owners allow just GoogleBot (and maybe BingBot), making it an extremely tedious process for an unknown crawler to get whitelisted on these sites. https://0x65.dev/blog/2019-12-06/building-a-search-engine-from-scratch.html
> We were told that this would take between 1 and 2 years to complete, and would cost a minimum of $1 billion (Again, this was 2013!). Needless to say, this was not a very enticing proposition. https://0x65.dev/blog/2019-12-05/a-new-search-engine.html
* _indexer_: writes/updates keys https://drewdevault.com/2020/11/17/Better-than-DuckDuckGo.html
* _vertical search_: Amazon, Kayak https://diff.substack.com/p/inside-the-house-report-on-big-tech-6a6
* alternative: Neeva, DuckDuckGo, Marginalia, Kagi, Andi https://dkb.io/post/the-next-google Elicit https://elicit.org/ Consensus https://consensus.app/search/
* no likes Google anymore https://www.newyorker.com/culture/infinite-scroll/what-google-search-isnt-showing-you
> Viktor Lofgren, a Swedish software developer and consultant who created his own indie search engine called Marginalia, told me, “One part of the sameyness is that recommendation and prediction algorithms often seem to work almost too well.” Marginalia, which Lofgren started working on a year ago, is a bare-bones Web site run entirely from a computer in his living room. The search engine’s stated mission is to “show you sites you perhaps weren’t aware of.” Its results, based on its own custom algorithm and data gathering, prioritize text-based Web sites that lack ads, mobile support, encryption, and other features that qualify as good S.E.O. “Google punishes sites that aren’t up to speed with modern Web technologies,” Lofgren said. “Legitimately old Web sites also deserve some attention.” A Marginalia search for “best toaster” brings up tech blogs from the nineties and vintage Internet jokes about technology companies of the day. (“If Apple made toasters . . . It would do everything Microsoft toaster does, but 5 years earlier.”) There are no images on the page, let alone carrousels or “Buy It Now” buttons. The Marginalia results would not help you choose a new appliance, but they are a fascinating glimpse into how much material the Internet contains, and how much never makes it to the top of current Google results.
* _robots.txt_`: file that tells crawlers what files to ignore https://adamj.eu/tech/2020/02/10/robots-tx
* _PageRank_: ranking algo that weights on number of incoming links (and their popularity)
* _instant answer_: display text from top result in overall results https://drewdevault.com/2020/11/17/Better-than-DuckDuckGo.html
* getting past SEO-induced homogenization https://news.ycombinator.com/item?id=23202850
* increasing AI-driven = specific queries work less well https://news.ycombinator.com/item?id=28113007
* blacklist https://github.com/davidahmed/wiper 
* Google mistaken identity https://news.ycombinator.com/item?id=28216733
* Yandex https://diff.substack.com/p/yandex-google-through-the-looking

🦆 DuckDuckGo
* search bar: `h`
* main result: `m`
* open link: `l`
* open link - new tab: `cmd return`
* bangs: amz (Amazon) dis (Discogs) g (Google) git (Github) hn (Hacker News) m (Google Maps) mwd (Merriam Webster) so (Stack Overflow) w (Wikipedia) xgau (Christgau) yt (Youtube) https://duckduckgo.com/bang

## spell checker

* https://spylls.readthedocs.io/en/latest/ https://zverok.github.io/blog/2021-05-06-how-to-spellcheck.html
* https://norvig.com/spell-correct.html
* https://theautomatic.net/2019/12/10/3-packages-to-build-a-spell-checker-in-python/
* https://0x65.dev/blog/2019-12-08/how-do-you-spell-boscodictiasaur.html

# ZA

* _y combinator_: https://news.ycombinator.com/item?id=27673177
* cellular automaton, Conway's game of life https://en.wikipedia.org/wiki/Cellular_automaton https://robertheaton.com/2018/07/20/project-2-game-of-life/
* _byte offset_: distance from initial byte to target; used to lookup char in file [Kleppmann 72]
* _intelligent music production_: using algos to mix? https://www.amazon.com/gp/product/B0815BWLXV
* randomness https://classic.qz.com/perfect-company-2/1172282/this-company-built-one-of-the-worlds-most-efficient-warehouses-by-embracing-chaos/
* _Naive Bayes_: priors + data; naive bc assume every feature has same weight [Bhargava 10.200]
* softmax https://victorzhou.com/blog/softmax/
* visualization in Jupyter https://kylekizirian.github.io/prims-algorithm.html

---

* _audio warping_: https://stackoverflow.com/q/9953219/6813490
* geography https://github.com/jftuga/geodist

## recursion

* _base case_: case in which the function doesn't call itself
* _recursive case_: case in which function calls itself
* _partial execution_: state of function when another function called from within it (until the other function completes its own execution) [3.44]
* _perf_: can be slow bc chewing up stack space [Code Complete 17.2, Bhargava 3.40]
* _tail_: can prevent stack overflows but depends on compiler to provide optimization https://stackoverflow.com/a/37010/6813490

```python
def countdown(arg):
    if arg == 0:
        return None
    else:
        countdown(arg - 1)

countdown(1)

""
first frame goes on stack
first frame blocks on else, calls `countdown(0)`
second frame `countdown(0)` goes on stack
second frame comes off stack
first frame stops blocking on else, comes off stack
"""
```

## regex

* _regex_: pattern to match sequence of characters
* _regular_: based on something called 'regular languages' https://stackoverflow.com/a/975495/6813490

* recipes
```sh
# starts with
^word
```

---

* flavors: PCRE2 (Perl) https://github.com/rust-lang/regex/issues/127
* BYO regex engine https://kean.blog/post/lets-build-regex
🛠 https://regex101.com/library https://zaiste.net/posts/shell-commands-rust/#grex https://github.com/pemistahl/grex#how-to-install-cli 

* why doesn't this work?
```sh
/U/z/D/z/m/z/p/m/b/method $ l | rg 1*.mp3

```
* _flags_: Python and JavaScript have https://docs.python.org/3/library/re.html#re.compile
* _multiline_: https://www.youtube.com/watch?v=ASa7jjRCLNI https://stackoverflow.com/a/587620/6813490
* _standards_: Vim vs. PCRE https://stackoverflow.com/questions/3864467/whats-the-difference-between-vim-regex-and-normal-regex
* _sink_: 🗄 `algos/python-regex.pdf` https://regexone.com/

__quantifiers__

* `\d`  == 1 digit
* `\d?` == 0 || == 1 https://regex101.com/r/XsAyxb/1 + https://regex101.com/r/C4Rg6L/1
* `\d*` >= 0
* `\d+` >= 1
* `[aeious]{2,}` >= 2
* `[aeiou]{2}` == 2 vowels
* `[aeious]{2, 5}` >= 3 && <= 5
 
__special characters__

```sh
# [] char set = match single https://regex101.com/r/EulQ8w/1
[aeiouAEIOU]
Ba  # match on 'a'

# - range
[0-9]  # match single char in range
123  # separate match for each of 1, 2, and 3
```

* `()` group https://regex101.com/r/SF2Mpd/4
* `\` escape
* `\b` boundary (`\bcat\b` 'black cat' `\bcat` 'catfish' `cat\b` 'tomcat')
* `{<num>}` repeat https://regex101.com/r/xYhGg4/1
* `|` or

* `^` exclude (when inside character set)
* `^` anchor to start (when outside character set)
* `$` anchor to end https://regex101.com/r/SF2Mpd/1

__metacharacters__

📝 capitalize for opposite

* `.` any char except new line
* `\s` white space (space, tab, new line)
* `\t` tab only
* `\d` for any num (`[0-9]`)
* `\w` any letter or num (`[a-zA-Z0-9]`]) -> also includes `_`
 