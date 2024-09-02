# CrowdFunding Smart Contract

This project is a simple crowdfunding smart contract written in Solidity. It allows users to create and manage crowdfunding campaigns, where others can donate Ether to support these campaigns.

## Features

- **Create Campaigns**: Users can create a new campaign by specifying details such as the title, description, target amount, deadline, and an image URL.
- **Donate to Campaigns**: Users can donate Ether to any active campaign.
- **Track Donations**: The contract keeps track of all donations and the donors for each campaign.
- **View Campaigns**: All campaigns can be viewed, including their details and the amount of funds collected.

## Contract Structure

### Campaign Struct

The `Campaign` struct contains the following fields:

- `owner`: The address of the campaign creator.
- `title`: The title of the campaign.
- `description`: A brief description of the campaign.
- `target`: The funding goal of the campaign in Ether.
- `deadline`: The deadline for the campaign to reach its funding goal.
- `amountCollected`: The total amount of Ether collected so far.
- `image`: A URL to an image representing the campaign.
- `donators`: An array of addresses that have donated to the campaign.
- `donations`: An array of donation amounts corresponding to the `donators`.

### Functions

#### `createCampaign`

```solidity
function createCampaign(
    address _owner,
    string memory _title,
    string memory _description,
    uint256 _target,
    uint256 _deadline,
    string memory _image
) public returns (uint256)
```

- Creates a new campaign with the specified details.
- Returns the ID of the newly created campaign.

#### `donateToCampaign`

```solidity
function donateToCampaign(uint256 _id) public payable
```

- Allows users to donate Ether to a specific campaign by its ID.
- The donation amount is transferred to the campaign owner’s address.

#### `getDonators`

```solidity
function getDonators(uint256 _id) view public returns (address[] memory, uint256[] memory)
```

- Returns the list of donators and their corresponding donation amounts for a given campaign.

#### `getCampaigns`

```solidity
function getCampaigns() public view returns (Campaign[] memory)
```

- Returns an array of all campaigns with their details.

## Usage

1. **Deploy the Contract**: Deploy the contract on the Ethereum network using your preferred method (Remix, Hardhat, etc.).
2. **Create a Campaign**: Call the `createCampaign` function with the necessary details.
3. **Donate to a Campaign**: Use the `donateToCampaign` function, specifying the campaign ID and sending Ether.
4. **View Campaigns**: Retrieve all campaigns and their details using the `getCampaigns` function.

## Example

```solidity
CrowdFunding crowdFunding = new CrowdFunding();

// Create a new campaign
uint256 campaignId = crowdFunding.createCampaign(
    msg.sender,
    "Save the Rainforest",
    "Help us save the Amazon rainforest from deforestation!",
    10 ether,
    block.timestamp + 30 days,
    "https://example.com/image.png"
);

// Donate to the campaign
crowdFunding.donateToCampaign{value: 1 ether}(campaignId);

// Get campaign details
(address[] memory donators, uint256[] memory donations) = crowdFunding.getDonators(campaignId);
```

## License

This project is licensed under the UNLICENSED License.
