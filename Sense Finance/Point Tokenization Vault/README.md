# Sense Finance Point Tokenization Vault - Security Assessment & Formal Verification

## Project Overview

### Project Summary
| Project Name  | Sense Finance Point Tokenization Vault |
| :--- | :--- |
| Language  | Solidity  |
| Codebase  | https://github.com/sense-finance/point-tokenization-vault |

### Project Description

Sense Finance Point Tokenization Vault allows users to make deposits, claim `PToken` tokens and redeem them for rewards. 

## Audit Overview

### Audit Summary
| Delivery Date  | Nov 5, 2025 |
| :--- | :--- |
| Audit Methodology          | Manual Review, Static Analysis, Formal Verification  |
| Author(s)                  | [Vladimir Ryzhak](https://www.ryzhak.com/)  |
| Final Commit               | [2e607155b234dcb69d1fbbe126f930bed779c134](https://github.com/sense-finance/point-tokenization-vault/tree/2e607155b234dcb69d1fbbe126f930bed779c134) |
| Formal Verification Report | [PToken.sol](https://prover.certora.com/output/8691664/c872f24c50ba450185fb556d0241c10a/?anonymousKey=e30987f3b2fc49454e94ddecdbd4767b214a1de9), [PointTokenVault.sol](https://prover.certora.com/output/8691664/23fd20f6bca64240b4972242bd81a220/?anonymousKey=92cb8631c9cf27eed20196f465705a6fbbc4ff4f)  |
| Formal Verification CI Setup | [PR URL](https://github.com/sense-finance/point-tokenization-vault/pull/68) |

### Audit Scope
| Filename  | URL |
| :--- | :--- |
| `PToken.sol` | https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol |
| `PointTokenVault.sol` | https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol |

### Severity Matrix

|        Severity        | Impact: High | Impact: Medium | Impact: Low |
| :--------------------: | :----------: | :------------: | :---------: |
|  **Likelihood: High**  |   Critical   |      High      |   Medium    |
| **Likelihood: Medium** |     High     |     Medium     |     Low     |
|  **Likelihood: Low**   |    Medium    |      Low       |     Low     |

#### Impact
- **High** - results in a considerable risk that may jeopardize the protocol's overall integrity, impacting all or the majority of users.
- **Medium** - results in a non-critical risk for the protocol, impacting either all users or a specific subset, yet remaining unequivocally unacceptable.
- **Low** - losses incurred will be within acceptable limits, attack vectors can be fixed with relative ease.

#### Likelihood
- **High** - highly probable, presenting significant financial opportunities for exploitation by malicious actors.
- **Medium** - still relatively probable, although contingent upon certain conditions.
- **Low** - requires a unique set of conditions and presents a cost of execution that does not yield a favorable ratio of rewards for the individual involved.

### Findings Summary
| Severity  | Discovered |
| :--- | :--- |
| Critical | - |
| High | - |
| Medium | 4 |
| Low | 1 |
| Total | 5 |

### Findings
| ID   | Title | Severity |
| :--- | :---  | :---     |
| M-01 | Operator can brick `PointTokenVault` for a particular `PToken` | Medium |
| M-02 | User may be unable to withdraw deposit if reward and deposit tokens are equal | Medium |
| M-03 | Infinite `PToken` mint in a corner case | Medium |
| M-04 | Some "weird" ERC20 tokens are not supported | Medium |
| L-01 | ETH can be stuck in the contract | Low |

## Certora Formal Verification

### Overview

| Contract  | Report URL |
| :--- | :--- |
| [PToken.sol](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol) | [Report URL](https://prover.certora.com/output/8691664/c872f24c50ba450185fb556d0241c10a/?anonymousKey=e30987f3b2fc49454e94ddecdbd4767b214a1de9) |
| [PointTokenVault.sol](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol) | [Report URL](https://prover.certora.com/output/8691664/23fd20f6bca64240b4972242bd81a220/?anonymousKey=92cb8631c9cf27eed20196f465705a6fbbc4ff4f) |

### Properties (PToken.sol)

| Property Description | Type| Passed |
| :--- | :--- | :---: |
| Total supply is sum of all balances | High | :white_check_mark: |
| Total supply never overflows | High | :white_check_mark: |
| Max number of balance changes in a single call is 2 | High | :white_check_mark: |
| Only `approve()` and `transferFrom()` can change allowance | High | :white_check_mark: |
| User balance may be changed only by: `mint()`, `burn()`, `transfer()`, `transferFrom()` | High | :white_check_mark: |
| Only `mint()` and `burn()` can change total supply | High | :white_check_mark: |
| Account's balance can be reduced only by token holder or approved 3rd party | High | :white_check_mark: |
| Only token holder can increase allowance, spender can decrease it by using it | High | :white_check_mark: |
| `mint()` updates storage as expected | Unit | :white_check_mark: |
| `mint()` reverts when expected | Unit | :white_check_mark: |
| `mint()` does not affect 3rd party | Unit | :white_check_mark: |
| `burn()` updates storage as expected | Unit | :white_check_mark: |
| `burn()` reverts when expected | Unit | :white_check_mark: |
| `burn()` does not affect 3rd party | Unit | :white_check_mark: |
| `transfer()` updates storage as expected | Unit | :white_check_mark: |
| `transfer()` of a single huge amount works the same as 2 transfers of small amounts | Unit | :white_check_mark: |
| `transfer()` reverts when expected | Unit | :white_check_mark: |
| `transfer()` does not affect 3rd party | Unit | :white_check_mark: |
| `transferFrom()` updates storage as expected | Unit | :white_check_mark: |
| `transferFrom()` reverts when expected | Unit | :white_check_mark: |
| `transferFrom()` does not affect 3rd party | Unit | :white_check_mark: |
| `transferFrom()` of a single huge amount works the same as 2 transfers of small amounts | Unit | :white_check_mark: |
| `approve()` updates storage as expected | Unit | :white_check_mark: |
| `approve()` reverts when expected | Unit | :white_check_mark: |
| `approve()` does not affect 3rd party | Unit | :white_check_mark: |
| `pause()` updates storage as expected | Unit | :white_check_mark: |
| `pause()` reverts when expected | Unit | :white_check_mark: |
| `unpause()` updates storage as expected | Unit | :white_check_mark: |
| `unpause()` reverts when expected | Unit | :white_check_mark: |

### Properties (PointTokenVault.sol)

| Property Description | Type| Passed |
| :--- | :--- | :---: |
| Methods are called by expected roles | High | :white_check_mark: |
| `deposit()` updates storage as expected | Unit | :white_check_mark: |
| `deposit()` reverts when expected | Unit | :white_check_mark: |
| `deposit()` does not affect other entities | Unit | :white_check_mark: |
| `withdraw()` updates storage as expected | Unit | :white_check_mark: |
| `withdraw()` reverts when expected | Unit | :white_check_mark: |
| `withdraw()` does not affect other entities | Unit | :white_check_mark: |
| `claimPTokens()` updates storage as expected | Unit | :white_check_mark: |
| `claimPTokens()` reverts when expected | Unit | :white_check_mark: |
| `claimPTokens()` does not affect other entities | Unit | :white_check_mark: |
| `redeemRewards()` updates storage as expected | Unit | :white_check_mark: |
| `redeemRewards()` reverts when expected | Unit | :white_check_mark: |
| `redeemRewards()` does not affect other entities | Unit | :white_check_mark: |
| `convertRewardsToPTokens()` updates storage as expected | Unit | :white_check_mark: |
| `convertRewardsToPTokens()` reverts when expected | Unit | :white_check_mark: |
| `convertRewardsToPTokens()` does not affect other entities | Unit | :white_check_mark: |
| `trustReceiver()` updates storage as expected | Unit | :white_check_mark: |
| `trustReceiver()` reverts when expected | Unit | :white_check_mark: |
| `deployPToken()` reverts when expected | Unit | :white_check_mark: |
| `updateRoot()` updates storage as expected | Unit | :white_check_mark: |
| `updateRoot()` reverts when expected | Unit | :white_check_mark: |
| `setCap()` updates storage as expected | Unit | :white_check_mark: |
| `setCap()` reverts when expected | Unit | :white_check_mark: |
| `setRedemption()` updates storage as expected | Unit | :white_check_mark: |
| `setRedemption()` reverts when expected | Unit | :white_check_mark: |
| `setMintFee()` updates storage as expected | Unit | :white_check_mark: |
| `setMintFee()` reverts when expected | Unit | :white_check_mark: |
| `setRedemptionFee()` updates storage as expected | Unit | :white_check_mark: |
| `setRedemptionFee()` reverts when expected | Unit | :white_check_mark: |
| `pausePToken()` updates storage as expected | Unit | :white_check_mark: |
| `pausePToken()` reverts when expected | Unit | :white_check_mark: |
| `unpausePToken()` updates storage as expected | Unit | :white_check_mark: |
| `unpausePToken()` reverts when expected | Unit | :white_check_mark: |
| `renouncePauseRole()` updates storage as expected | Unit | :white_check_mark: |
| `renouncePauseRole()` reverts when expected | Unit | :white_check_mark: |
| `collectFees()` updates storage as expected | Unit | :white_check_mark: |
| `collectFees()` reverts when expected | Unit | :white_check_mark: |
| `collectFees()` does not affect other entities | Unit | :white_check_mark: |
| `setFeeCollector()` updates storage as expected | Unit | :white_check_mark: |
| `setFeeCollector()` reverts when expected | Unit | :white_check_mark: |

## Findings

### [M-01] Operator can brick `PointTokenVault` for a particular `PToken`

#### Description
Operator is able to pause a particular `PToken` contract and renounce the `PAUSE_ROLE` from the `PointTokenVault` contract 
which will cause DoS for most of the methods.

Example:
1. Operator [pauses](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L344) a particular `PToken`
2. Operator [removes](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L352) the `PAUSE_ROLE` from the `PointTokenVault` contract

At this point operator can no longer [unpause](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L348) the `PToken` since the `PointTokenVault` contract doesn't have the `PAUSE_ROLE` anymore.

Additionally the following methods would always revert since `PToken` is paused and `PointTokenVault` is missing the `PAUSE_ROLE`:
- [PToken.mint()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol#L21)
- [PToken.burn()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol#L25)
- [PToken.transferFrom()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol#L29)
- [PToken.transfer()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol#L33)
- [PointTokenVault.claimPTokens()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L147)
- [PointTokenVault.redeemRewards()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L177)
- [PointTokenVault.convertRewardsToPTokens()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L241)
- [PointTokenVault.pausePToken()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L344)
- [PointTokenVault.unpausePToken()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L348)
- [PointTokenVault.collectFees()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L356)

#### PoC
```solidity
// SPDX-License-Identifier: AGPL-3.0-only
pragma solidity =0.8.24;

import {ERC1967Proxy} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol";
import {Test, console, console2} from "forge-std/Test.sol";
import {MockERC20, ERC20} from "solmate/test/utils/mocks/MockERC20.sol";
import {FixedPointMathLib} from "solmate/utils/FixedPointMathLib.sol";
import {PToken} from "../../PToken.sol";
import {PointTokenVault} from "../../PointTokenVault.sol";

contract ProtocolTest is Test {
    PointTokenVault pointTokenVaultImplementation;
    ERC1967Proxy proxy;
    PointTokenVault pointTokenVault;

    MockERC20 usdtToken;
    MockERC20 rewardToken;

    address admin = makeAddr("admin");
    address feeCollector = makeAddr("feeCollector");
    address user = makeAddr("user");
    address user2 = makeAddr("user2");
    address user3 = makeAddr("user3");

    function setUp() public {
        pointTokenVaultImplementation = new PointTokenVault();
        bytes memory initData = abi.encodeWithSignature("initialize(address,address)", admin, feeCollector);
        proxy = new ERC1967Proxy(address(pointTokenVaultImplementation), initData);
        pointTokenVault = PointTokenVault(payable(address(proxy)));

        usdtToken = new MockERC20("USDT", "USDT", 18);
        usdtToken.mint(user, 100 ether);

        rewardToken = new MockERC20("RWD", "RWD", 18);
        rewardToken.mint(address(pointTokenVault), 100 ether);

        vm.startPrank(user);
        usdtToken.approve(address(pointTokenVault), type(uint256).max);
        rewardToken.approve(address(pointTokenVault), type(uint256).max);
        vm.stopPrank();

        vm.startPrank(admin);
        pointTokenVault.grantRole(pointTokenVault.OPERATOR_ROLE(), admin);
        pointTokenVault.grantRole(pointTokenVault.MERKLE_UPDATER_ROLE(), admin);
        pointTokenVault.setCap(address(usdtToken), type(uint256).max);
        pointTokenVault.setMintFee(0.1e18); // 10%
        pointTokenVault.setRedemptionFee(0.1e18); // 10%
        pointTokenVault.setFeeCollector(feeCollector);
        vm.stopPrank();
    }

    /**
     * Scenario:
     * 1. `OPERATOR_ROLE` pauses pToken
     * 2. `OPERATOR_ROLE` calls `renouncePauseRole()` which removes `PAUSE_ROLE` from `PointTokenVault`
     * 3. `OPERATOR_ROLE` tries to unpause pToken which reverts with `AccessControlUnauthorizedAccount` since
     * `PointTokenVault` doesn't have the `PAUSE_ROLE` anymore thus causing DoS for:
     * - PToken.mint()
     * - PToken.burn()
     * - PToken.transferFrom()
     * - PToken.transfer()
     * - PointTokenVault.claimPTokens()
     * - PointTokenVault.redeemRewards()
     * - PointTokenVault.convertRewardsToPTokens()
     * - PointTokenVault.pausePToken()
     * - PointTokenVault.unpausePToken()
     * - PointTokenVault.collectFees()
     */
    function testRenouncePauseRole() public {
        // deploy PToken
        bytes32 pTokenId = keccak256("pointsId1");
        PToken pToken = pointTokenVault.deployPToken(pTokenId);

        vm.startPrank(admin);
        pointTokenVault.pausePToken(pTokenId);
        pointTokenVault.renouncePauseRole(pTokenId);
        // reverts with `AccessControlUnauthorizedAccount` causing DoS for most of `PToken` and `PointTokenVault` methods
        pointTokenVault.unpausePToken(pTokenId);
        vm.stopPrank();
    }
}
```

#### Recommendation
In `PToken` [constructor](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PToken.sol#L13) grant `DEFAULT_ADMIN_ROLE` to `msg.sender`. This way, in case of emergency, `PointTokenVault` could be upgraded to manage `PToken` roles.

---

### [M-02] User may be unable to withdraw deposit if reward and deposit tokens are equal

#### Description
If deposit and reward tokens are equal user may be unable to call [withdraw()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L134).

Example:
1. User1 deposits 100 USDT
2. Admins sets redemption params so that deposit and reward tokens are the same
3. User2 buys 100 PTokens on secondary market
4. User2 calls `redeemRewards()` burning 100 PTokens for 90 USDT (-10% redemption fee)
5. User1 is unable to call `withdraw()` since there's not enough funds

#### PoC
```solidity
// SPDX-License-Identifier: AGPL-3.0-only
pragma solidity =0.8.24;

import {ERC1967Proxy} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol";
import {Test, console, console2} from "forge-std/Test.sol";
import {MockERC20, ERC20} from "solmate/test/utils/mocks/MockERC20.sol";
import {FixedPointMathLib} from "solmate/utils/FixedPointMathLib.sol";
import {PToken} from "../../PToken.sol";
import {PointTokenVault} from "../../PointTokenVault.sol";

contract ProtocolTest is Test {
    PointTokenVault pointTokenVaultImplementation;
    ERC1967Proxy proxy;
    PointTokenVault pointTokenVault;

    MockERC20 usdtToken;
    MockERC20 rewardToken;

    address admin = makeAddr("admin");
    address feeCollector = makeAddr("feeCollector");
    address user = makeAddr("user");
    address user2 = makeAddr("user2");
    address user3 = makeAddr("user3");

    function setUp() public {
        pointTokenVaultImplementation = new PointTokenVault();
        bytes memory initData = abi.encodeWithSignature("initialize(address,address)", admin, feeCollector);
        proxy = new ERC1967Proxy(address(pointTokenVaultImplementation), initData);
        pointTokenVault = PointTokenVault(payable(address(proxy)));

        usdtToken = new MockERC20("USDT", "USDT", 18);
        usdtToken.mint(user, 100 ether);

        rewardToken = new MockERC20("RWD", "RWD", 18);
        rewardToken.mint(address(pointTokenVault), 100 ether);

        vm.startPrank(user);
        usdtToken.approve(address(pointTokenVault), type(uint256).max);
        rewardToken.approve(address(pointTokenVault), type(uint256).max);
        vm.stopPrank();

        vm.startPrank(admin);
        pointTokenVault.grantRole(pointTokenVault.OPERATOR_ROLE(), admin);
        pointTokenVault.grantRole(pointTokenVault.MERKLE_UPDATER_ROLE(), admin);
        pointTokenVault.setCap(address(usdtToken), type(uint256).max);
        pointTokenVault.setMintFee(0.1e18); // 10%
        pointTokenVault.setRedemptionFee(0.1e18); // 10%
        pointTokenVault.setFeeCollector(feeCollector);
        vm.stopPrank();
    }

    /**
     * Scenario:
     * 1. User1 deposits 100 USDT
     * 2. Admins sets redemption params so that deposit and reward tokens are the same
     * 3. User2 buys 100 PTokens on secondary market
     * 4. User2 calls `redeemRewards()` burning 100 PTokens for 90 USDT (-10% redemption fee)
     *.5. User1 is unable to call `withdraw()` since there's not enough funds
     */
    function testRewardAndDepositTokensAreTheSame() public {
        // deployPToken
        bytes32 pTokenId = keccak256("pointsId1");
        PToken pToken = pointTokenVault.deployPToken(pTokenId);

        // deposit
        vm.prank(user);
        pointTokenVault.deposit(usdtToken, 100 ether, user);

        // setRedemption
        vm.prank(admin);
        pointTokenVault.setRedemption(pTokenId, usdtToken, 1 ether, false);

        // user2 buys 100 PTokens on secondary market
        deal(address(pToken), user2, 100 ether);

        // redeemRewards
        bytes32[] memory proof = new bytes32[](1);
        proof[0] = "";
        PointTokenVault.Claim memory claim = PointTokenVault.Claim({
            pointsId: pTokenId,
            totalClaimable: 100 ether,
            amountToClaim: 100 ether,
            proof: proof
        });
        vm.prank(user2);
        pointTokenVault.redeemRewards(claim, user2);

        // withdraw reverts with "not enough funds"
        vm.prank(user);
        vm.expectRevert();
        pointTokenVault.withdraw(usdtToken, 100 ether, user);
    }
}
```

#### Recommendation
Don't allow deposit and reward tokens to be equal.

---

### [M-03] Infinite `PToken` mint in a corner case

#### Description
If [reward token](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L64) is a `PToken` then, on certrain conditions, user can infinitely mint `PTokens`.

Example:
1. Admin sets `PToken` as a reward token with `0.5 ether` as a reward per `PToken`
2. User calls `convertRewardsToPTokens()`, transfers 10 `PTokens` and gets 20 `PTokens` minted
3. At his point user can repeat steps 1 and 2 which is basically an infinite mint

#### PoC
```solidity
// SPDX-License-Identifier: AGPL-3.0-only
pragma solidity =0.8.24;

import {ERC1967Proxy} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol";
import {Test, console, console2} from "forge-std/Test.sol";
import {MockERC20, ERC20} from "solmate/test/utils/mocks/MockERC20.sol";
import {FixedPointMathLib} from "solmate/utils/FixedPointMathLib.sol";
import {PToken} from "../../PToken.sol";
import {PointTokenVault} from "../../PointTokenVault.sol";

contract ProtocolTest is Test {
    PointTokenVault pointTokenVaultImplementation;
    ERC1967Proxy proxy;
    PointTokenVault pointTokenVault;

    MockERC20 usdtToken;
    MockERC20 rewardToken;

    address admin = makeAddr("admin");
    address feeCollector = makeAddr("feeCollector");
    address user = makeAddr("user");
    address user2 = makeAddr("user2");
    address user3 = makeAddr("user3");

    function setUp() public {
        pointTokenVaultImplementation = new PointTokenVault();
        bytes memory initData = abi.encodeWithSignature("initialize(address,address)", admin, feeCollector);
        proxy = new ERC1967Proxy(address(pointTokenVaultImplementation), initData);
        pointTokenVault = PointTokenVault(payable(address(proxy)));

        usdtToken = new MockERC20("USDT", "USDT", 18);
        usdtToken.mint(user, 100 ether);

        rewardToken = new MockERC20("RWD", "RWD", 18);
        rewardToken.mint(address(pointTokenVault), 100 ether);

        vm.startPrank(user);
        usdtToken.approve(address(pointTokenVault), type(uint256).max);
        rewardToken.approve(address(pointTokenVault), type(uint256).max);
        vm.stopPrank();

        vm.startPrank(admin);
        pointTokenVault.grantRole(pointTokenVault.OPERATOR_ROLE(), admin);
        pointTokenVault.grantRole(pointTokenVault.MERKLE_UPDATER_ROLE(), admin);
        pointTokenVault.setCap(address(usdtToken), type(uint256).max);
        pointTokenVault.setMintFee(0.1e18); // 10%
        pointTokenVault.setRedemptionFee(0.1e18); // 10%
        pointTokenVault.setFeeCollector(feeCollector);
        vm.stopPrank();
    }

    /**
     * Scenario:
     1. Admin sets PToken as a reward token with `0.5 ether` as a reward per PToken
     2. User calls `convertRewardsToPTokens()`, transfers 10 PTokens and gets 20 PTokens minted
     3. At his point user can repeat steps 1 and 2 which is basically an infinite mint
     */
    function testConvertRewardsToPTokens() public {
        // deployPToken
        bytes32 pTokenId = keccak256("pointsId1");
        PToken pToken = pointTokenVault.deployPToken(pTokenId);

        // setRedemption
        vm.prank(admin);
        pointTokenVault.setRedemption(pTokenId, pToken, 0.5 ether, false);
        
        deal(address(pToken), user, 10 ether);

        // convertRewardsToPTokens
        vm.startPrank(user);
        pToken.approve(address(pointTokenVault), type(uint256).max);
        pointTokenVault.convertRewardsToPTokens(user, pTokenId, 10 ether);
        vm.stopPrank();

        // user got 20 PTokens for transferring 10 PTokens
        assertEq(pToken.balanceOf(user), 20 ether);
    }
}
```

#### Recommendation
Don't allow reward token to be `PToken`.

---

### [M-04] Some "weird" ERC20 tokens are not supported

#### Description
There are [many](https://github.com/d-xo/weird-erc20) "weird" ERC20 tokens which behave differently from "standard" ERC20 tokens. For example, some have fees on transfer while others are able to rebase token balances.

Some of those tokens must not be used as a deposit or reward token because it breaks the `PointTokenVault` contract leading to DoS or unexpected behavior.

For example, if there're fees on deposit token transfer then there will be a difference between the deposited amount in storage and the actual amount in contract [here](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L126).

Here's the list of compatibility between the `PointTokenVault` contract and "weird" ERC20 tokens:
|               | Deposit Token | Reward Token |
| ------------- | :-----------: | :----------: |
| [Reentrant Calls](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#reentrant-calls)  |:white_check_mark:|:white_check_mark:|
| [Missing Return Values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values) |:white_check_mark:|:white_check_mark:|
| [Fee on Transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer) |:x:|:x:|
| [Rebasing](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) |:x:|:x:|
| [Upgradable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens) |:white_check_mark:|:white_check_mark:|
| [Flash Mintable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens) |:white_check_mark:|:white_check_mark:|
| [Tokens with Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists) |:x:|:x:|
| [Pausable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens) |:x:|:x:|
| [Approval Race Protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections) |:white_check_mark:|:white_check_mark:|
| [Revert on Approval To Zero Address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address) |:white_check_mark:|:white_check_mark:|
| [Revert on Zero Value Approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals) |:white_check_mark:|:white_check_mark:|
| [Revert on Zero Value Transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers) |:white_check_mark:|:white_check_mark:|
| [Multiple Token Addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#multiple-token-addresses) |:white_check_mark:|:white_check_mark:|
| [Low Decimals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals) |:white_check_mark:|:white_check_mark:|
| [High Decimals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals) |:white_check_mark:|:white_check_mark:|
| [transferFrom with src == msg.sender](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#transferfrom-with-src--msgsender) |:white_check_mark:|:white_check_mark:|
| [Non string metadata](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#non-string-metadata) |:white_check_mark:|:white_check_mark:|
| [Revert on Transfer to the Zero Address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address) |:white_check_mark:|:white_check_mark:|
| [No Revert on Failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure) |:white_check_mark:|:white_check_mark:|
| [Revert on Large Approvals & Transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers) |:white_check_mark:|:white_check_mark:|
| [Code Injection Via Token Name](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#code-injection-via-token-name) |:white_check_mark:|:white_check_mark:|
| [Unusual Permit Function](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#unusual-permit-function) |:white_check_mark:|:white_check_mark:|
| [Transfer of less than amount](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#transfer-of-less-than-amount) |:x:|:x:|
| [ERC-20 Representation of Native Currency](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#erc-20-representation-of-native-currency) |:white_check_mark:|:white_check_mark:|

#### Recommendation
If you plan to add a new reward token make sure it's compatible with the current `PointTokenVault` contract. Also you could whitelist deposit tokens and allow only the compatible ones.

---

### [L-01] ETH can be stuck in the contract

#### Description

There's the [receive()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L403) method which means that contract can accept `ETH`. The thing is that there's no way to withdraw it anyhow so all sent `ETH` will be stuck in the contract.

#### Recommendation
Remove the [receive()](https://github.com/sense-finance/point-tokenization-vault/blob/2e607155b234dcb69d1fbbe126f930bed779c134/contracts/PointTokenVault.sol#L403) method.

---

## Disclaimer
This security review should not be interpreted as providing absolute assurance against potential hacks or exploits. Smart contracts represent a novel technological advancement, inherently associated with various known and unknown risks. The protocol for which this report is prepared indemnifies the author from any liability concerning potential misbehavior, bugs, or exploits affecting the audited code throughout the entirety of the project's life cycle. It is also crucial to recognize that any modifications made to the audited code, including remedial measures for the issues outlined in this report, may inadvertently introduce new complications and necessitate further auditing.

## About the author
Prepared by [ryzhak.com](https://www.ryzhak.com/).

Perform a comprehensive smart contract audit using advanced formal verification tools that identify even the most elusive and intricate bugs within smart contracts and mathematically prove the absence of security issues. All formal verification properties will be integrated into your standard deployment CI/CD pipelines, which helps reduce the number of bugs in already audited code, thereby lowering costs for future security assessments.
