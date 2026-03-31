# Custom-Error-Handling
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CustomErrors {
    error InsufficientBalance(uint256 available, uint256 required);
    error Unauthorized(address caller);
    error InvalidInput(string reason);

    uint256 public balance;

    function deposit(uint256 amount) public {
        if (amount == 0) revert InvalidInput("Amount must be > 0");
        balance += amount;
    }

    function withdraw(uint256 amount) public {
        if (balance < amount) revert InsufficientBalance(balance, amount);
        balance -= amount;
        payable(msg.sender).transfer(amount);
    }
}
