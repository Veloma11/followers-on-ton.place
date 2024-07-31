# followers-on-ton.place
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TonPlaceFollowers {
    // Структура для хранения подписчиков
    struct User {
        uint256 followerCount;
        mapping(address => bool) followers;
    }

    // Маппинг для хранения информации о пользователях
    mapping(address => User) private users;

    // Событие для добавления подписчика
    event FollowerAdded(address indexed user, address indexed follower);

    // Событие для удаления подписчика
    event FollowerRemoved(address indexed user, address indexed follower);

    // Функция для добавления подписчика
    function addFollower(address user) public {
        require(user != msg.sender, "You cannot follow yourself");
        require(!users[user].followers[msg.sender], "Already following this user");

        users[user].followers[msg.sender] = true;
        users[user].followerCount += 1;

        emit FollowerAdded(user, msg.sender);
    }

    // Функция для удаления подписчика
    function removeFollower(address user) public {
        require(users[user].followers[msg.sender], "Not following this user");

        users[user].followers[msg.sender] = false;
        users[user].followerCount -= 1;

        emit FollowerRemoved(user, msg.sender);
    }

    // Функция для получения количества подписчиков
    function getFollowerCount(address user) public view returns (uint256) {
        return users[user].follower
mkdir tonplace-followers
cd tonplace-followers
npx hardhat
// scripts/deploy.js
async function main() {
  const [deployer] = await ethers.getSigners();

  console.log("Deploying contracts with the account:", deployer.address);

  const TonPlaceFollowers = await ethers.getContractFactory("TonPlaceFollowers");
  const tonPlaceFollowers = await TonPlaceFollowers.deploy();

  console.log("TonPlaceFollowers deployed to:", tonPlaceFollowers.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
npx hardhat run scripts/deploy.js --network ropsten
