# Satlayer Deposit Contract - Security Assessment & Formal Verification

## Project Overview

### Project Summary
| Project Name  | Satlayer Deposit Contract |
| :--- | :--- |
| Language  | Solidity  |
| Codebase  | https://github.com/satlayer/deposit-contract-public |

### Project Description

Satlayer Deposit Contract allows users to deposit wrapped bitcoin assets in exchange for receipt tokens. Users with active deposits can later migrate their staked assets to the Satlayer mainnet network.

## Audit Overview

### Audit Summary
| Delivery Date  | Oct 13, 2025 |
| :--- | :--- |
| Audit Methodology          | Manual Review, Static Analysis, Formal Verification  |
| Author(s)                  | [Vladimir Ryzhak](https://www.ryzhak.com/) |
| Final Commit               | [1dd233d6dda3991234bc5ed6e0477b22a2570e04](https://github.com/satlayer/deposit-contract-public/tree/1dd233d6dda3991234bc5ed6e0477b22a2570e04) |
| Formal Verification Report | [ReceiptToken.sol](https://prover.certora.com/output/8691664/2283f9e590ab48aca2f9e14fbe31124e/?anonymousKey=58a5d6e15d8f2c89c188ab8baff453a618d7abea), [SatlayerPool.sol](https://prover.certora.com/output/8691664/c7912732329b4601971ed9b85f37db9f/?anonymousKey=05824e30d8d74d94bd65665d1bcd0723611ac968) |
| Formal Verification CI Setup | [PR URL](https://github.com/satlayer/deposit-contract-public/pull/1) |

### Audit Scope
| Filename  | URL |
| :--- | :--- |
| `ReceiptToken.sol` | https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/ReceiptToken.sol |
| `SatlayerPool.sol` | https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol |

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
| Medium | - |
| Low | 6 |
| Total | 6 |

### Findings
| ID   | Title | Severity |
| :--- | :---  | :---     |
| L-01 | Griefing by frontrunning `withdraw()` and `migrate()` methods | Low |
| L-02 | Receipt tokens can be stuck in the `SatlayerPool` contract | Low |
| L-03 | Some "weird" ERC20 tokens are not supported | Low |
| L-04 | When `approve()` returns false the contract should revert | Low |
| L-05 | The `_decimals` property should be immutable | Low |
| L-06 | Error not used | Low |

## Certora Formal Verification

### Overview

| Contract  | Report URL |
| :--- | :--- |
| [ReceiptToken.sol](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/ReceiptToken.sol) | [Report URL](https://prover.certora.com/output/8691664/2283f9e590ab48aca2f9e14fbe31124e/?anonymousKey=58a5d6e15d8f2c89c188ab8baff453a618d7abea) |
| [SatlayerPool.sol](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol) | [Report URL](https://prover.certora.com/output/8691664/c7912732329b4601971ed9b85f37db9f/?anonymousKey=05824e30d8d74d94bd65665d1bcd0723611ac968) |

### Properties (ReceiptToken.sol)

| Property Description | Type| Passed |
| :--- | :--- | :---: |
| Total supply is sum of all balances | High | :white_check_mark: |
| Balance of `address(0)` is 0 | High | :white_check_mark: |
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

### Properties (SatlayerPool.sol)

| Property Description | Type| Passed |
| :--- | :--- | :---: |
| `tokenAllowlist` updates are restricted to certain roles and methods | High | :white_check_mark: |
| `tokenMap` updates are restricted to certain roles and methods | High | :white_check_mark: |
| `capsEnabled` updates are restricted to certain roles and methods | High | :white_check_mark: |
| `caps` updates are restricted to certain roles and methods | High | :white_check_mark: |
| `migrator` updates are restricted to certain roles and methods | High | :white_check_mark: |
| `eventId` only increases & updates are restricted to certain roles and methods | High | :white_check_mark: |
| `onlyOwner` protected methods can be called only by contract owner | High | :white_check_mark: |
| `whenNotPaused` protected methods always revert if contract is paused | High | :white_check_mark: |
| `depositFor()` updates storage as expected | Unit | :white_check_mark: |
| `depositFor()` reverts when expected | Unit | :white_check_mark: |
| `depositFor()` does not affect other entities | Unit | :white_check_mark: |
| `withdraw()` updates storage as expected | Unit | :white_check_mark: |
| `withdraw()` reverts when expected | Unit | :white_check_mark: |
| `withdraw()` does not affect other entities | Unit | :white_check_mark: |
| `migrate()` updates storage as expected | Unit | :white_check_mark: |
| `migrate()` reverts when expected | Unit | :white_check_mark: |
| `migrate()` does not affect other entities | Unit | :white_check_mark: |
| `setCapsEnabled()` updates storage as expected | Unit | :white_check_mark: |
| `setCapsEnabled()` reverts when expected | Unit | :white_check_mark: |
| `setMigrator()` updates storage as expected | Unit | :white_check_mark: |
| `setMigrator()` reverts when expected | Unit | :white_check_mark: |
| `addToken()` updates storage as expected | Unit | :white_check_mark: |
| `addToken()` reverts when expected | Unit | :white_check_mark: |
| `setTokenStakingParams()` updates storage as expected | Unit | :white_check_mark: |
| `setTokenStakingParams()` reverts when expected | Unit | :white_check_mark: |
| `pause()` updates storage as expected | Unit | :white_check_mark: |
| `pause()` reverts when expected | Unit | :white_check_mark: |
| `unpause()` updates storage as expected | Unit | :white_check_mark: |
| `unpause()` reverts when expected | Unit | :white_check_mark: |
| `recoverERC20()` updates storage as expected | Unit | :white_check_mark: |
| `recoverERC20()` reverts when expected | Unit | :white_check_mark: |
| `recoverERC20()` does not affect other entities | Unit | :white_check_mark: |
| `renounceOwnership()` reverts when expected | Unit | :white_check_mark: |

## Findings

### [L-01] Griefing by frontrunning `withdraw()` and `migrate()` methods

#### Description
Malicious user can frontrun [withdraw()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L71) and [migrate()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L86) methods causing DoS for a user who wants to withdraw or migrate a stake.

Example:
1. User A stakes 100 stake tokens and gets 100 receipt tokens
2. User A tries to [withdraw()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L71) or [migrate()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L86) 100 stake tokens
3. User B (malicious) buys 100 receipt tokens on a secondary market, frontruns User A's transaction and withdraws or migrates stake tokens for himself
4. At his point [SatlayerPool](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol) has 0 stake token balance hence User A's transaction will revert with "out of funds"

#### Recommendation
Refactor the code to forbid users without a stake to call [withdraw()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L71) and [migrate()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L86) methods.

---

### [L-02] Receipt tokens can be stuck in the `SatlayerPool` contract

#### Description
Consider an example:
1. Owner adds a new stake token (`STK`) and a corresponding receipt token `RCT_0`
2. Owner adds `RCT_0` receipt token as a stake token
3. User stakes 100 `STK` tokens setting the [_for](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L53) parameter to the `SatlayerPool` contract which gets 100 `RCT_0`
4. Those 100 `RCT_0` are stuck in the contract since [recoverERC20()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L189) reverts with the `TokenAlreadyAdded` error

#### PoC
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.24;

import "forge-std/Test.sol";
import "forge-std/console2.sol";
import {IMigrator} from "../../src/interface/IMigrator.sol";
import {ReceiptToken} from "../../src/ReceiptToken.sol";
import {SatlayerPool} from "../../src/SatlayerPool.sol";

contract MockMigrator is IMigrator {
    function migrate(
        address _user,
        string calldata _destinationAddress, 
        address[] calldata _tokens,
        uint256[] calldata _amounts
    ) external {}
}

contract ProtocolTest is Test {
    ReceiptToken stakeToken;
    ReceiptToken stakeToken2;
    SatlayerPool satlayerPool;
    MockMigrator mockMigrator;

    address owner = makeAddr("owner");
    address user = makeAddr("user");
    address user2 = makeAddr("user2");

    function setUp() public {
        vm.startPrank(owner);
        
        stakeToken = new ReceiptToken("STK", "STK", 18);
        stakeToken2 = new ReceiptToken("STK_2", "STK_2", 18);

        address[] memory tokensAllowed = new address[](1);
        tokensAllowed[0] = address(stakeToken);
        uint256[] memory caps = new uint256[](1);
        caps[0] = 1000 ether;
        string[] memory names = new string[](1); // receipt token names
        names[0] = "RCT_0";
        string[] memory symbols = new string[](1); // receipt token symbols
        symbols[0] = "RCT_0";
        satlayerPool = new SatlayerPool(tokensAllowed, caps, names, symbols);

        mockMigrator = new MockMigrator();

        vm.stopPrank();
    }

    /**
     * Funds are stuck:
     * 1. Owner adds a new stake token (`STK`) and a corresponding receipt token `RCT_0`
     * 2. Owner adds `RCT_0` token as a stake token
     * 3. User stakes 100 `STK` setting staking recipient to be `SatlayerPool` which gets 100 `RCT_0`
     * 4. Those 100 `RCT_0` are stuck in the contract since `recoverERC20()` reverts with `TokenAlreadyAdded`
     */
    function test_ReceiptTokensStuck() public {
        vm.prank(owner);
        stakeToken.mint(user, 100 ether);

        // owner adds receipt token as a stake token
        vm.startPrank(owner);
        satlayerPool.addToken(satlayerPool.tokenMap(address(stakeToken)), 1000 ether, "RCT_0", "RCT_0");
        vm.stopPrank();

        // user stakes 100 STK tokens setting receiver to be `SatlayerPool`
        vm.startPrank(user);
        stakeToken.approve(address(satlayerPool), type(uint256).max);
        satlayerPool.depositFor(address(stakeToken), address(satlayerPool), 100 ether);
        vm.stopPrank();

        // Owner tries to recover RCT_0 tokens mistakenly sent to `SatlayerPool`.
        // `recoverERC20()` reverts and RCT_0 tokens are stuck in the contract.
        vm.startPrank(owner);
        satlayerPool.recoverERC20(satlayerPool.tokenMap(address(stakeToken)), owner, 100 ether);
        vm.stopPrank();
    }
}
```

#### Recommendation
In the [addToken()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L138) method validate that added token is not a receipt token.

---

### [L-03] Some "weird" ERC20 tokens are not supported

#### Description
There are [many](https://github.com/d-xo/weird-erc20) "weird" ERC20 tokens which behave differently from "standard" ERC20 tokens. For example, some have fees on transfer while others are able to rebase token balances.

Some of those tokens should not be used as a deposit token in the [SatlayerPool](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol) contract because it leads to DoS or unexpected behavior.

For example, ERC20 tokens with callbacks (like `ERC777`) will allow to circumvent the [cap limit](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L57) while pausable tokens and tokens with blacklist functionality will DoS users' withdrawals.

Here's the list of compatibility between the `SatlayerPool` contract and "weird" ERC20 tokens:
|               | Deposit Token |
| ------------- | :-----------: |
| [Reentrant Calls](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#reentrant-calls)  |:x:|
| [Missing Return Values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values) |:white_check_mark:|
| [Fee on Transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer) |:white_check_mark:|
| [Rebasing](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) |:white_check_mark:|
| [Upgradable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens) |:white_check_mark:|
| [Flash Mintable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens) |:white_check_mark:|
| [Tokens with Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists) |:x:|
| [Pausable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens) |:x:|
| [Approval Race Protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections) |:white_check_mark:|
| [Revert on Approval To Zero Address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address) |:white_check_mark:|
| [Revert on Zero Value Approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals) |:white_check_mark:|
| [Revert on Zero Value Transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers) |:white_check_mark:|
| [Multiple Token Addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#multiple-token-addresses) |:white_check_mark:|
| [Low Decimals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals) |:white_check_mark:|
| [High Decimals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals) |:white_check_mark:|
| [transferFrom with src == msg.sender](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#transferfrom-with-src--msgsender) |:white_check_mark:|
| [Non string metadata](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#non-string-metadata) |:white_check_mark:|
| [Revert on Transfer to the Zero Address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address) |:white_check_mark:|
| [No Revert on Failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure) |:white_check_mark:|
| [Revert on Large Approvals & Transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers) |:x:|
| [Code Injection Via Token Name](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#code-injection-via-token-name) |:white_check_mark:|
| [Unusual Permit Function](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#unusual-permit-function) |:white_check_mark:|
| [Transfer of less than amount](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#transfer-of-less-than-amount) |:white_check_mark:|
| [ERC-20 Representation of Native Currency](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#erc-20-representation-of-native-currency) |:white_check_mark:|

And here is the list of compatibility of tokens expected to be used as deposit ones and their features which might not be compatible with the `SatlayerPool` contract:
| | pumpBTC | WBTC | uniBTC | LBTC | solvBTC.BBN | waBTC | SBTC | stBTC | FBTC |
| ------------- | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: |
|[Reentrant Calls](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#reentrant-calls)| :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |
|[Tokens with Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists)| :negative_squared_cross_mark: | :negative_squared_cross_mark: |  :heavy_exclamation_mark: |  :negative_squared_cross_mark: |  :heavy_exclamation_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |
|[Pausable Tokens](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens)| :negative_squared_cross_mark: | :heavy_exclamation_mark: |  :negative_squared_cross_mark: |  :heavy_exclamation_mark: |  :negative_squared_cross_mark: |  :heavy_exclamation_mark: |  :heavy_exclamation_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |
|[Revert on Large Approvals & Transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers)| :negative_squared_cross_mark: | :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |  :negative_squared_cross_mark: |

#### Recommendation
If you plan to add a new deposit token make sure it's compatible with the current `SatlayerPool` contract.

---

### [L-04] When `approve()` returns false the contract should revert

#### Description
The interface of this [approve()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L101) method returns `false` in case approval failed. Not all ERC20 tokens revert on failed approval so it makes sense to check the return value and revert in case it is `false`.

#### Recommendation
Revert in case the [approve()](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/SatlayerPool.sol#L101) method returned `false`.

---

### [L-05] The `_decimals` property should be immutable

#### Description
The [_decimals](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/ReceiptToken.sol#L13) property should be marked as `immutable` in order to save gas.

#### Recommendation
Mark the [_decimals](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/ReceiptToken.sol#L13) property as `immutable`.

---

### [L-06] Error not used

#### Description
The [TokenAlreadyConfiguredWithState](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/interface/ISatlayerPool.sol#L18) error is not used anywhere, remove it.

#### Recommendation
Remove the [TokenAlreadyConfiguredWithState](https://github.com/satlayer/deposit-contract-public/blob/1dd233d6dda3991234bc5ed6e0477b22a2570e04/src/interface/ISatlayerPool.sol#L18) error.

---

## Disclaimer
This security review should not be interpreted as providing absolute assurance against potential hacks or exploits. Smart contracts represent a novel technological advancement, inherently associated with various known and unknown risks. The protocol for which this report is prepared indemnifies the author from any liability concerning potential misbehavior, bugs, or exploits affecting the audited code throughout the entirety of the project's life cycle. It is also crucial to recognize that any modifications made to the audited code, including remedial measures for the issues outlined in this report, may inadvertently introduce new complications and necessitate further auditing.

## About the author
Prepared by [ryzhak.com](https://www.ryzhak.com/).

Perform a comprehensive smart contract audit using advanced formal verification tools that identify even the most elusive and intricate bugs within smart contracts and mathematically prove the absence of security issues. All formal verification properties will be integrated into your standard deployment CI/CD pipelines, which helps reduce the number of bugs in already audited code, thereby lowering costs for future security assessments.
