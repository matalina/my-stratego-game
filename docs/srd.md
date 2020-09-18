# System Requirements Document

2 players  
10x10 board with 2 2x2 areas in the center creating choke points

|   | A | B | C | D | E | F | G | H | I | J |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 |   |   |   |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   |   |   |   |
| 3 |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   | X | X |   |   | X | X |   |   |
| 5 |   |   | X | X |   |   | X | X |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |
| 7 |   |   |   |   |   |   |   |   |   |   |
| 8 |   |   |   |   |   |   |   |   |   |   |
| 9 |   |   |   |   |   |   |   |   |   |   |

Pieces
| Name       | R | # | Exceptions |
|------------|---|---|------------|
| Bomb       | B | 6 | cannot move, caputurable by Miner |
| Marshal    | 1 | 1 | can be captured by attacking spy |
| General    | 2 | 1 |  |
| Colonel    | 3 | 2 |  |
| Major      | 4 | 3 |  |
| Captain    | 5 | 4 |  |
| Lieutenant | 6 | 4 |  |
| Sergant    | 7 | 4 |  |
| Miner      | 8 | 5 | Difuse bombs |
| Scout      | 9 | 8 | move any number of spaces in straight light without jumping |
| Spy        | S | 1 | defeats marshal if attacking |
| Flag       | F | 1 | cannot move, if captured loses game |
