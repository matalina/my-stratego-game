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

Player - use default JetStream object/database  

Basic Game
```
class Game {
  Board board; 
  Player red_player;
  Player blue_player;
  Tray red_tray;
  Tray blue_tray;
  
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

Pieces Basics
```
class Piece {
  integer id;
  string color; // red or blue
  integer type_id; // type of Piece
  
  function moveTo(tile_id);
  function attack(piece_id);
  function die();
}

class PieceType {
  integer id;
  string name;
  string abbr;
  string icon;
  
  integer rank; // 0 = Bomb, 1-9, 10 = spy, 99 = flag
  
  boolean move_many; // defaults false (except Scout/9)
  boolean can_move; // defaults true (except flag/F/99 and bomb/B/0)
  boolean take_rank_1; // defaults to false (except spy/S/10)
  boolean difuse_bomb; // defaults to false (except miner/8)
  boolean win_game; // defaults to false (except flat/F/99)
}

class Tray {
  string color;
  array pieces;
  
  function setup();
  function placePieceOn(piece_id, tile_id);
  function takePieceFrom(piece_id, tile_id);
  function stats(); // displays number of peices total and per piece
}
```

Basic Log Entries
```
Game {
  integer id;
  datetime created_at;
  integer red_player; // player_id
  integer blue_player; // player_id
  json board; // description of board and tiles
  json pieces; // description of peices
}

Move {
  integer id;
  integer game_id;
  integer player_id;
  datetime moved_at;
  integer piece_moved; // piece_id
  integer moved_from; // tile_id
  interger moved_to; // tile_id
  boolean attacked; 
  boolean win; // null if attacked is false
  integer against_peice; // piece_id null if attacked is false
}

Chat {
  integer id;
  integer player_id;
  integer game_id;
  datetime said_at;
  text message;
}
```

### Stats to calculate

* number of wins
* number of loses
* number of draws
* number of bombs hit
* number of bombes difused
* number of times captured a marshal
* number of times your marshal was captured
* number of moves in shortest game
* number of moves in longest game

# Psuedo Code
board.js
```js
let Board = {
  board: [],
  
  options: {
    rows: 10,
    cols: 10
  },
  
  row_names: ['A','B','C','D','E','F','G','H','I','J','K','L','M'
    ,'N','O','P','Q','R','S','T','U','V','W','X','Y','Z],
  
  setup(options = {}) {   
    for(let index in options) {
      if(this.options[index] !== undefined) {
        this.options[index] = options[index];
    }
    
    for(let r = 0; r < this.options.rows; r++) {
      let letter = this.row_names[r];
      if(this.board[r] === undefined) {
        this.board[r] = [];
      }
      for(let c = 0; r < this.options.columns; c++) {
        let number = c + 1;
        this.board[letter][number] = (Object.create(Tile)).init(letter, number, this.options);
      }
    }
    return this;
  }
}
```
