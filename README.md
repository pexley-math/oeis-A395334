# Counting polyominoes with a fully surrounded cell

*Peter Exley, Independent Researcher, Brisbane, Australia. Submitted: Jun 16 2026.*

Take a shape made of unit squares joined edge to edge. Each square has four edges,
so up to four neighbors. Call a square *surrounded* when all four of its neighbors
are present in the shape, so it sits in the interior with nothing of its boundary
exposed. The smallest shape with a surrounded square is the plus-pentomino: a
center square with one square on each side. We ask how many n-square shapes contain
at least one surrounded square, and count them.

## The problem

A polyomino is a finite, edge-connected set of unit squares on the square grid.
The free polyominoes of n cells are these shapes counted up to the symmetries of
the square -- its rotations and reflections, the dihedral group of order eight.
They are counted by OEIS A000105.

A cell of a polyomino has up to four edge-neighbors on the grid. Call a cell
*saturated* when all four of its neighbors also belong to the polyomino, so the
cell is completely surrounded. We count the polyominoes that have at least one such
cell: `a(n)` is the number of free polyominoes of n cells containing a saturated
cell. This is a new sequence.

## Definitions

A *cell* is a unit square of the grid, named by its integer coordinates. Two cells
are *edge-adjacent* when they share an edge; each cell has up to four
edge-neighbors. A *polyomino* is a set of cells connected through edge-adjacency.
It is *free* when shapes related by a rotation or reflection of the square are
regarded as the same.

A cell is *saturated* when all four of its edge-neighbors belong to the polyomino.
A saturated cell is an interior cell: nothing of its boundary is exposed. A
polyomino *has a saturated cell* when at least one of its cells is saturated. This
needs at least five cells -- the saturated cell plus its four neighbors -- so the
first four terms are zero, and the first qualifying shape is the plus-pentomino at
n = 5.

The shapes with no saturated cell form the complementary count
c(n) = A000105(n) - a(n) = 1, 1, 2, 5, 11, 33, 99, 333, 1128, ...; these are the
thin, tree-like, and holey shapes whose every cell keeps an exposed edge. Neither
a(n) nor c(n) appears in the OEIS.

A390515 is a related but distinct family: the free polyominoes in which every cell
carries one specified, oriented chipped edge that cannot connect, where two chipped
edges may meet as long as the shape stays connected through the unchipped edges. It
is not the complement c(n). There a missing neighbor is an unmarked structural
property of the shape; in A390515 the chipped edge is a labeled, oriented feature of
each cell, so the two count different things.

## Companion sequences

The same question on the other two regular lattices gives a matching pair. A395331
counts the polyiamonds with a saturated cell on the triangular lattice, where a cell
has three edge-neighbors and four cells already suffice. A395552 counts the polyhexes
on the hexagonal lattice, where a cell has six edge-neighbors, so a saturated cell
needs seven cells and first appears later. The three sequences share one definition
read on three lattices, and the proportion of saturated shapes rises fastest on the
triangular lattice and slowest on the hexagonal one.

## The values

**Result.** The number of free polyominoes of n cells that contain a saturated
cell, for n = 1 to 14, is:

| n | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| a(n) | 0 | 0 | 0 | 0 | 1 | 2 | 9 | 36 | 157 | 667 | 2852 | 12081 | 50786 | 211971 |

The shapes for the first several n are drawn in the gallery
[`figures.pdf`](figures.pdf). The single saturated shape at n = 5 is the
plus-pentomino; as n grows the saturated shapes fill out into compact blocks, since
a compact block of squares quickly traps a cell on all four sides.

## How we know

We enumerate the free polyominoes directly and keep those with a saturated cell.
Each shape is grown one cell at a time from a single starting square, and recorded
once using a canonical form under the eight symmetries of the square. Testing
whether a shape has a saturated cell is immediate: scan its cells for one whose four
edge-neighbors are all present. The enumeration grows from a single square over the
whole plane with no bounding region, so the count is exact and unconditional --
there is no search window that could miss a shape.

Two independent counts must agree before we accept a value. The first grows the
free shapes, identifying rotations and reflections as it goes, and filters them. The
second grows the fixed shapes -- distinguishing translations only -- filters those,
and recovers the free count through the orbit-counting relation, which adds the
symmetry sizes of the free shapes and must equal the fixed total. The two paths
share no bookkeeping, so a discrepancy would expose an error in either. The same
enumeration without the saturation filter reproduces the full free-polyomino count
A000105 (1, 1, 2, 5, 12, 35, 108, 369, 1285, 4655, ...) at every n, tying our work
to a published count before the filter is applied. A separate program, sharing no
code, computes every value a third way. All checks agree across the whole range.

## Patterns and open questions

The counts grow quickly, the ratio of consecutive terms climbing toward the growth
rate of the polyomino family as a whole, near 4.

The fraction a(n) / A000105(n) -- the proportion of free polyominoes with a
saturated cell -- rises steadily but slowly: 0.08,
0.06, 0.08, 0.10, 0.12, 0.14, 0.17, 0.19, 0.21, 0.24 for n = 5 to 14. It climbs
much more gradually than for the triangular analogue, where a cell needs only three
present neighbors rather than four, so interiors appear later on the square grid. The proportion nevertheless tends to 1.
By Madras's pattern theorem for lattice clusters (1999), a fully surrounded cell is a
local pattern that occurs in the interior of large polyominoes, so all but an
exponentially small fraction of n-cell polyominoes contain at least one. Almost every
large polyomino is therefore saturated, the shapes with no surrounded cell become a
vanishing minority, and a(n) shares the exponential growth rate of A000105(n). The
approach to 1 is slow, consistent with the modest value at n = 14.

One fact is settled: a(n) < A000105(n) for every n, because the straight strip of n
cells never surrounds a cell, so a shape with no saturated cell always exists.

We computed fourteen terms. The fifteenth lies just out of reach: the number of
shapes to examine roughly quadruples at each step, and at n = 15 the enumeration
exceeds our memory budget. No polynomial, finite recurrence, or closed form fits the
values, which is expected for a count of this kind.

## Further reading

This work was inspired by the OEIS and the community of contributors who maintain
it.

- Madras, N. (1999). "A pattern theorem for lattice clusters." Annals of Combinatorics, 3, 357-384. (arXiv:math/9902161)
- Redelmeier, D. H. (1981). "Counting polyominoes: yet another attack." Discrete Mathematics, 36(2), 191-203.
- Sloane, N. J. A. "A000105: Number of free polyominoes (or square animals) with n cells." The On-Line Encyclopedia of Integer Sequences. https://oeis.org/A000105

## License

[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) -- see `LICENSE`. This work is freely available; a citation or acknowledgment is appreciated but not required.
