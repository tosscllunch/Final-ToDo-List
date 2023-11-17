# Final-ToDo-List

Ethereum Blockchain Application - Todo List
This is a straightforward todo list application powered by smart contracts, offering an insightful exploration into blockchain technology and decentralized platforms. Unlike traditional todo list applications, the data, including todo list items, is not stored in a central database but distributed across the blockchain network.

Technologies Used:
Solidity - High-level language for implementing Smart Contracts
Truffle Framework - Ethereum DApps
Metamask Ethereum Wallet - Chrome Extension
web3.js - Library for interacting with Ethereum blockchain
Node.js
Deployment

# Install dependencies 
$ npm install -g truffle@5.0.2
$ npm install

# Migrate 
truffle migrate --reset

# Run the app
$ npm run dev
Task Management Features:
The task management system is modeled using a struct and mapping state variable within the TodoList.sol smart contract. This allows for efficient look-up of any task by its unique identifier.

solidity

// TodoList.sol
pragma solidity ^0.5.0;

contract TodoList {
  uint public taskCount = 0;

  struct Task {
    uint id;
    string content;
    bool completed;
  }

  mapping(uint => Task) public tasks;
}
Creating and Completing Tasks:
The smart contract provides functions for creating tasks, with each task triggering an event, and completing tasks, updating the smart contract accordingly.

solidity

// TodoList.sol
pragma solidity ^0.5.0;

contract TodoList {

  // ...

  event TaskCreated(
    uint id,
    string content,
    bool completed
  );

  // ...

  function createTask(string memory _content) public {
    taskCount ++;
    tasks[taskCount] = Task(taskCount, _content, false);
    emit TaskCreated(taskCount, _content, false);
  }

  // ...

  function toggleCompleted(uint _id) public {
    Task memory _task = tasks[_id];
    _task.completed = !_task.completed;
    tasks[_id] = _task;
    emit TaskCompleted(_id, _task.completed);
  }
}
Testing:
Testing of the application can be performed using the Truffle testing framework.

# Run Test 
$ truffle test 
Local Blockchain Simulation and Metamask Integration:
The development environment includes Ganache, a local blockchain for testing smart contracts, and Metamask, a Chrome extension that serves as an Ethereum wallet. These tools facilitate the deployment, development, and testing of the application.
