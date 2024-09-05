# Rock Paper Scissors Game - Aptos Blockchain

This project is a decentralized application (dApp) built on the Aptos blockchain. It allows users to play a classic game of Rock Paper Scissors, with moves and results managed by a smart contract deployed on the Aptos testnet. The game uses randomness generated by the Aptos Roll API to simulate the computer's move.

## Features
- **Frontend GUI**: Players can access dapp gui to play the game.
- **Wallet Integration**: Players can connect their Aptos-compatible wallet (e.g., Pontem or Petra) to play the game.
- **Random Computer Moves**: The dApp uses Aptos Roll for generating randomness to determine the computer's move.
- **Game Tracking**: The dApp tracks player wins, computer wins, draws, and total games played.
- **Endless Gameplay**: Players can restart the game after each round and continue playing without refreshing the page.

## Technologies Used

- **Frontend**: React.js
- **Vite development tool**
- **Blockchain SDK**: Aptos TypeScript SDK (`@aptos-labs/ts-sdk`)
- **Wallet Adapter**: Aptos Wallet Adapter (`@aptos-labs/wallet-adapter-react`)
- **CSS**: Basic responsive UI with custom styles

 

## Installation and Setup

To run this project locally, follow these steps:

### Prerequisites

- Node.js installed (v16+ recommended)
- Aptos Wallet (e.g., Petra) installed in your browser
- Git installed

### Clone the Repository

```bash
 git clone https://github.com/Im-in123/aptos-dapp-rock-paper-scissors
 cd aptos-dapp-rock-paper-scissors
 npm install
 npm run dev
```
 

## How to Play

1. **Connect Wallet**: Click "Connect Wallet" to connect your Aptos-compatible wallet (e.g., Petra).
2. **Start Game**: Once your wallet is connected, click "Start Game" to initialize the game.
3. **Choose Your Move**: After the game starts, select either Rock, Paper, or Scissors.
4. **Submit Move**: After selecting your move, click "Shoot!" to submit your move.
5. **View Results**: The computer's move and the game outcome will be displayed. You can then choose to "Play Again" or reload the result.
6. **Track Scores**: The total wins, losses, and draws will be updated automatically after each round.

## Smart Contract Interaction

The game interacts with the Aptos blockchain via a Move contract, which includes the following functions:

- `start_game`: Initializes a new game.
- `set_player_move`: Sets the player’s move (Rock, Paper, or Scissors).
- `randomly_set_computer_move`: Uses the Aptos Roll randomness API to set the computer’s move.
- `finalize_game_results`: Finalizes the game results and determines the outcome (player win, computer win, or draw).
- `get_game_results`: Retrieves the game results.



## Smart Contract Address

The smart contract is deployed on the Aptos testnet:
0x3d44defa4494387906bb88b5f1f9ff1a0c1d4d59d036e709c06b0024a979f111


## Smart Contract Functions

### Game Management

- **`start_game(account: &signer)`**: Initializes a new game or resets an existing game. Also initializes `GameScore` if it doesn’t already exist.
- **`set_player_move(account: &signer, player_move: u8)`**: Sets the player's move (Rock, Paper, or Scissors). Prevents setting the move if the game has already been finalized.
- **`randomly_set_computer_move(account: &signer)`**: Sets the computer's move using the Aptos Roll randomness API. Uses the `#[randomness]` attribute for randomness.
- **`finalize_game_results(account: &signer)`**: Finalizes the game results and updates the score based on the outcome.

### Game Logic

- **`determine_winner(player_move: u8, computer_move: u8): u8`**: Determines the winner based on the player's and computer's moves. Returns:
  - `2` for player win
  - `1` for a draw
  - `3` for computer win

### View Functions

- **`get_player_move(account_addr: address): u8`**: Retrieves the player's move.
- **`get_computer_move(account_addr: address): u8`**: Retrieves the computer's move.
- **`get_game_results(account_addr: address): u8`**: Retrieves the game result.
- **`view_game_score(account_addr: address): (u64, u64, u64)`**: Retrieves the player's score including wins, computer wins, and games played.

## Improvements from Original Contract

- **Added Score Tracking**: The updated contract now tracks and maintains the player’s wins, losses, and games played with the `GameScore` struct.
- **Simplified Initialization**: The `start_game` function now directly initializes the game state and also initializes `GameScore` if it does not exist.
- **Removed Manual Reset**: The contract no longer requires manual game state reset functionality as it now initializes or updates the game state directly.
