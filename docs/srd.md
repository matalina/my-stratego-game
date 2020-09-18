# System Requirements Document

2 players  
10x10 board with 2 2x2 areas in the center creating choke points

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| A |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |
| E |   |   | X | X |   |   | X | X |   |   |
| F |   |   | X | X |   |   | X | X |   |   |
| G |   |   |   |   |   |   |   |   |   |   |
| H |   |   |   |   |   |   |   |   |   |   |
| I |   |   |   |   |   |   |   |   |   |   |
| J |   |   |   |   |   |   |   |   |   |   |

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

One move per turn.   
All pieces move 1 space vertically or horizontally at a time unless otherwise stated.  
Cannot move back and forth between two spaces more than three times  
Pieces may not share the same space.
On attack: Lower # wins. If the attacker wins they take the square  
Capturing the opponent flag wins the game  

## Objects

Basic Game
```
class Game {
  Board board; 
  Player red_player;
  Player blue_player;
  Tray red_tray;
  Tray blue_tray;
  Log game_log;
  Chat chat_log;
  
  function start();
  function pause();
  function withdraw();
}
```

Game Board
```
class Board {
  Array board; // 10x10 array of Tiles
  
  function setup();
}

class Tile {
  integer id;
  string name; // A0 - J9
  string col;
  string row;
  
  string image; //
  
  Array directions; // [u, r, d, l] tile_ids
  Piece piece; // null if empty;
  
  function canMove(tile_id);
  function isEmpty(); // is the tile empty? (return false or Piece)
  function clear();
  function hold(piece);
}
``` 

Tray (x2)  
Pieces (40 x2)  
Player (x2)  
Stats  
Logs  
Move  
