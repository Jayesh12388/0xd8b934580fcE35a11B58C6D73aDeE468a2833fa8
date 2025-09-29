/ SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Play2EarnGalaxy {
    address public owner;

    struct Player {
        uint256 earnedTokens;
        bool registered;
    }

    mapping(address => Player) public players;

    event PlayerRegistered(address indexed player);
    event TokensEarned(address indexed player, uint256 amount);
    event TokensWithdrawn(address indexed player, uint256 amount);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function registerPlayer() external {
        require(!players[msg.sender].registered, "Already registered");
        players[msg.sender] = Player({earnedTokens: 0, registered: true});
        emit PlayerRegistered(msg.sender);
    }

    function earnTokens(uint256 amount) external {
        require(players[msg.sender].registered, "Not registered");
        require(amount > 0, "Amount must be > 0");
        players[msg.sender].earnedTokens += amount;
        emit TokensEarned(msg.sender, amount);
    }

    function withdrawTokens() external {
        require(players[msg.sender].registered, "Not registered");
        uint256 earned = players[msg.sender].earnedTokens;
        require(earned > 0, "No tokens to withdraw");

        players[msg.sender].earnedTokens = 0;
        // In real scenario, tokens would be transferred here
        emit TokensWithdrawn(msg.sender, earned);
    }
}
