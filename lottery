// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BasicLottery {
    address[] public players;
    address public winner;
    bool public isLotteryOpen = true;

    // Join the lottery
    function enter() public payable {
        require(isLotteryOpen, "Lottery is closed");
        require(msg.value == 0.01 ether, "Entry fee is 0.01 ETH");
        players.push(msg.sender);
    }

    // Only allow winner to be picked once and only if there are players
    function pickWinner() public {
        require(isLotteryOpen, "Winner already selected");
        require(players.length > 0, "No players in the lottery");

        uint index = random() % players.length;
        winner = players[index];
        isLotteryOpen = false;

        // Send contract balance to the winner
        payable(winner).transfer(address(this).balance);
    }

    // Pseudo-random number generator (not secure for production)
    function random() private view returns (uint) {
        return uint(keccak256(abi.encodePacked(block.timestamp, block.difficulty, players)));
    }

    // View all players
    function getPlayers() public view returns (address[] memory) {
        return players;
    }
}
