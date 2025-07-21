# Milestone-Based Crowdfunding Smart Contract

A decentralized crowdfunding platform built on Stacks that revolutionizes project funding through milestone-based fund releases and community governance.

## 🌟 Overview

This smart contract addresses the fundamental trust issues in traditional crowdfunding platforms by implementing a milestone-based fund release system. Instead of releasing all funds upfront, funds are released incrementally as project creators achieve predefined milestones that are verified by the contributor community.

## 🎯 Key Features

### 1. **Milestone-Based Fund Release**
- Project creators define 1-10 milestones for their project
- Each milestone specifies a percentage of total funds to be released
- Funds remain locked in the contract until milestones are approved
- Sequential milestone completion ensures project progression

### 2. **Community-Driven Verification**
- Contributors vote on milestone completion
- Configurable approval thresholds (50-100% of contributors)
- Democratic process ensures quality delivery
- One vote per contributor per milestone prevents manipulation

### 3. **Contributor Protection**
- Automatic refunds for cancelled or expired projects
- Partial refunds based on uncompleted milestones
- Transparent fund tracking
- Withdrawal mechanisms for failed projects

### 4. **Platform Sustainability**
- Configurable platform fee (default: 2.5%)
- Fees only collected on successfully released funds
- Admin controls for fee adjustment
- Sustainable revenue model for platform maintenance

## 🚀 Getting Started

### Prerequisites
- [Clarinet](https://github.com/hirosystems/clarinet) installed
- Basic understanding of Clarity smart contracts
- STX tokens for testing

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd skillchain
```

2. Install dependencies:
```bash
clarinet integrate
```

3. Run tests:
```bash
clarinet test
```

## 📖 Contract Functions

### Project Management

#### `create-project`
Creates a new crowdfunding project.

**Parameters:**
- `title`: Project title (max 100 characters)
- `description`: Project description (max 500 characters)
- `funding-goal`: Target funding amount in microSTX
- `deadline`: Block height deadline for funding
- `milestone-count`: Number of milestones (1-10)

**Example:**
```clarity
(contract-call? .crowdfunding create-project 
    "DeFi Dashboard" 
    "A comprehensive analytics dashboard for DeFi protocols"
    u50000000000 ;; 50,000 STX
    u144000 ;; ~100 days from now
    u4) ;; 4 milestones
```

#### `add-milestone`
Adds a milestone to an existing project.

**Parameters:**
- `project-id`: The project ID
- `milestone-id`: Sequential milestone number
- `title`: Milestone title
- `description`: What will be delivered
- `funding-percentage`: Percentage of funds to release (basis points)
- `votes-required`: Required approval percentage (basis points)

**Example:**
```clarity
(contract-call? .crowdfunding add-milestone 
    u1 
    u1 
    "MVP Launch" 
    "Basic dashboard with core features"
    u2500 ;; 25% of funds
    u6000) ;; 60% approval required
```

### Contributing

#### `contribute`
Contribute STX to a project.

**Parameters:**
- `project-id`: The project to support
- `amount`: Amount in microSTX

**Example:**
```clarity
(contract-call? .crowdfunding contribute u1 u1000000000) ;; Contribute 1,000 STX
```

### Voting

#### `vote-on-milestone`
Vote on milestone completion.

**Parameters:**
- `project-id`: The project ID
- `milestone-id`: The milestone to vote on
- `approve`: true to approve, false to reject

**Example:**
```clarity
(contract-call? .crowdfunding vote-on-milestone u1 u1 true)
```

### Fund Management

#### `withdraw-contribution`
Withdraw funds from cancelled or expired projects.

**Parameters:**
- `project-id`: The project to withdraw from

#### `cancel-project`
Cancel a project (creator only, before any milestone completion).

**Parameters:**
- `project-id`: The project to cancel

## 📊 Read-Only Functions

### `get-project`
Retrieve complete project information.

### `get-milestone`
Get details about a specific milestone.

### `get-contribution`
Check a user's contribution to a project.

### `calculate-milestone-approval`
Calculate the current approval percentage for a milestone.

### `get-platform-fee`
Get the current platform fee percentage.

## 🔐 Security Features

1. **Access Control**
   - Only project creators can add milestones and cancel projects
   - Only contributors can vote on milestones
   - Only contract owner can adjust platform fees

2. **State Validation**
   - Projects cannot be funded after deadline
   - Milestones must be completed sequentially
   - Votes cannot be changed once cast
   - Cancelled projects cannot accept new contributions

3. **Fund Safety**
   - All funds held in contract until release conditions met
   - Automatic refund mechanisms
   - Platform fees only on successful releases
   - No unauthorized withdrawals possible

## 💡 Use Cases

1. **Software Development Projects**
   - Milestone 1: Design and Architecture (20%)
   - Milestone 2: MVP Development (30%)
   - Milestone 3: Testing and Security Audit (25%)
   - Milestone 4: Launch and Documentation (25%)

2. **Creative Projects**
   - Milestone 1: Concept and Pre-production (15%)
   - Milestone 2: Production Phase 1 (35%)
   - Milestone 3: Production Phase 2 (35%)
   - Milestone 4: Post-production and Delivery (15%)

3. **Research Projects**
   - Milestone 1: Literature Review and Methodology (20%)
   - Milestone 2: Data Collection (30%)
   - Milestone 3: Analysis and Results (30%)
   - Milestone 4: Publication and Dissemination (20%)

## 🛠️ Development

### Testing
```bash
# Run all tests
clarinet test

# Run specific test
clarinet test tests/crowdfunding_test.ts
```

### Deployment
```bash
# Deploy to testnet
clarinet deploy --testnet

# Deploy to mainnet
clarinet deploy --mainnet
```

## 📈 Platform Economics

- **Default Platform Fee**: 2.5% of released funds
- **Maximum Platform Fee**: 10% (hardcoded limit)
- **Fee Collection**: Only on successfully completed milestones
- **No fees on**: Refunds, cancelled projects, or failed milestones

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🚨 Disclaimer

This smart contract is provided as-is. While it has been designed with security in mind, it should undergo thorough testing and auditing before mainnet deployment. Users interact with this contract at their own risk.

## 📞 Support

For questions, issues, or contributions:
- Open an issue in the GitHub repository
- Contact the development team
- Join our Discord community

## 🗺️ Roadmap

- [ ] Multi-signature milestone approval
- [ ] Milestone evidence upload (IPFS integration)
- [ ] Partial milestone completion
- [ ] Milestone deadline enforcement
- [ ] Contributor reputation system
- [ ] Project categories and discovery
- [ ] Integration with Stacks NFTs for contributor badges

---

Built with ❤️ on Stacks
