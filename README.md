# Solidity Style Guide

- [Solidity Style Guide](#solidity-style-guide)
  - [Introduction](#introduction)
    - [Purpose and Scope](#purpose-and-scope)
    - [Evolution of the Guide](#evolution-of-the-guide)
    - [Consistency over Correctness](#consistency-over-correctness)
  - [General Coding Conventions](#general-coding-conventions)
    - [Indentation and Spacing](#indentation-and-spacing)
      - [Indentation Rules](#indentation-rules)
      - [Tabs or Spaces](#tabs-or-spaces)
      - [Blank Lines](#blank-lines)
      - [Maximum Line Length](#maximum-line-length)
      - [Source File Encoding](#source-file-encoding)
    - [Use the Latest Version of Solidity](#use-the-latest-version-of-solidity)
    - [Imports](#imports)
  - [Code Structure](#code-structure)
    - [Code Layout](#code-layout)
    - [Order of Functions](#order-of-functions)
    - [Order of Layout Elements](#order-of-layout-elements)
    - [Single Contract or Interface Per File](#single-contract-or-interface-per-file)
  - [Naming Conventions](#naming-conventions)
    - [Naming Styles](#naming-styles)
    - [Names to Avoid](#names-to-avoid)
    - [Contract and Library Names](#contract-and-library-names)
    - [Naming Interfaces](#naming-interfaces)
    - [Defining Contract Types in Interfaces](#defining-contract-types-in-interfaces)
    - [Struct Names](#struct-names)
    - [Event Names](#event-names)
    - [Function Names](#function-names)
    - [Variable Names](#variable-names)
    - [Function Argument Names](#function-argument-names)
    - [Constants](#constants)
    - [Modifier Names](#modifier-names)
    - [Enums](#enums)
    - [Avoiding Naming Collisions](#avoiding-naming-collisions)
    - [Underscore Prefix for Non-external Functions and Variables](#underscore-prefix-for-non-external-functions-and-variables)
  - [Code Formatting](#code-formatting)
    - [Whitespace in Expressions](#whitespace-in-expressions)
    - [Control Structures](#control-structures)
    - [Function Declarations](#function-declarations)
    - [Mappings](#mappings)
    - [Variable Declarations](#variable-declarations)
    - [Strings](#strings)
    - [Operators](#operators)
  - [Documentation](#documentation)
    - [NatSpec Documentation](#natspec-documentation)
  - [Best Practices](#best-practices)
    - [Using Custom Errors Over Require](#using-custom-errors-over-require)
    - [Require with Custom Error (Solidity 0.8.26+)](#require-with-custom-error-solidity-0826)
    - [Limit Require Messages](#limit-require-messages)
    - [Calldata for Read-Only Function Parameters](#calldata-for-read-only-function-parameters)
    - [Optimize Length in Loops](#optimize-length-in-loops)
    - [Prefer Named Return](#prefer-named-return)
    - [Prefer Named Arguments](#prefer-named-arguments)
    - [Prefer Named Parameters in Mapping Types](#prefer-named-parameters-in-mapping-types)
    - [Enforcing Explicit Types](#enforcing-explicit-types)
    - [Internal Function Naming](#internal-function-naming)
    - [Contract Interactions Through Interfaces](#contract-interactions-through-interfaces)
    - [Errors](#errors)
    - [Events](#events)
    - [Struct, Event and Error Definitions](#struct-event-and-error-definitions)
    - [Upgradability](#upgradability)
    - [Avoid Unnecessary Version Pragma Constraints](#avoid-unnecessary-version-pragma-constraints)
    - [Avoid Using Assembly](#avoid-using-assembly)
    - [Prefer Composition Over Inheritance](#prefer-composition-over-inheritance)
  - [Testing (Foundry Specific)](#testing-foundry-specific)
    - [Test Structure](#test-structure)
    - [Unit Tests](#unit-tests)
    - [Test Fixtures](#test-fixtures)
    - [Mocking and Stubbing](#mocking-and-stubbing)
    - [Property-Based Testing](#property-based-testing)
    - [Gas Usage Testing](#gas-usage-testing)
    - [Foundry Tools and Utilities](#foundry-tools-and-utilities)
    - [General Test Guidance](#general-test-guidance)
  - [Performance and Security](#performance-and-security)
    - [Gas Optimization](#gas-optimization)
    - [Security Best Practices](#security-best-practices)
      - [Reentrancy](#reentrancy)
      - [Access Control](#access-control)
      - [Integer Overflow and Underflow](#integer-overflow-and-underflow)
      - [Handling Ether Transfers](#handling-ether-transfers)
    - [Code Reviews and Audits](#code-reviews-and-audits)
  - [Conclusion](#conclusion)

### Introduction

#### Purpose and Scope

This guide is designed to provide coding conventions for writing Solidity code, ensuring consistency and readability. It is an evolving document that will adapt over time as new conventions are established and old ones become obsolete.

> [!NOTE]
> This guide is intended to extend, not replace, the official Solidity style guide, covering additional important aspects not addressed by the existing guidelines .

#### Evolution of the Guide

As Solidity and its ecosystem evolve, so too will this style guide. It will incorporate new best practices, discard outdated ones, and adapt to the changing needs of the community.

> [!TIP]
> 💡 Regular updates ensure that the guide remains relevant and continues to promote the latest best practices in Solidity development .

#### Consistency over Correctness

The primary goal of this guide is consistency, not necessarily correctness or the best way to write Solidity code. Consistency helps improve the readability and maintainability of codebases.

> [!IMPORTANT]
> "A foolish consistency is the hobgoblin of little minds." Consistency with this guide is important, but consistency within a project or module is even more crucial. Use your best judgment and adapt as necessary .

This introductory section sets the stage for a comprehensive style guide, emphasizing the importance of adaptability, consistency, and extending existing best practices in Solidity coding.

### General Coding Conventions

#### Indentation and Spacing

##### Indentation Rules

Use 4 spaces per indentation level.

> [!TIP]
> 💡 Consistent indentation enhances code readability and structure, making it easier to follow and maintain.

##### Tabs or Spaces

Spaces are the preferred indentation method. Avoid mixing tabs and spaces.

> [!WARNING]
> ⚠️ Mixing tabs and spaces can lead to hard-to-debug errors. Stick to spaces for consistency.

##### Blank Lines

- Surround top-level declarations in Solidity with two blank lines.
- Use a single blank line to separate function definitions within a contract.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
    // ...
}

contract B {
    // ...
}

contract C {
    // ...
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
    // ...
}
contract B {
    // ...
}

contract C {
    // ...
}
```

Within a contract, surround function declarations with a single blank line. Blank lines may be omitted between groups of related one-liners (such as stub functions for an abstract contract).

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract A {
    function spam() public virtual pure;
    function ham() public virtual pure;
}

contract B is A {
    function spam() public pure override {
        // ...
    }

    function ham() public pure override {
        // ...
    }
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract A {
    function spam() virtual pure public;
    function ham() public virtual pure;
}

contract B is A {
    function spam() public pure override {
        // ...
    }
    function ham() public pure override {
        // ...
    }
}
```

> [!IMPORTANT]
> Proper spacing helps visually separate different sections of your code, making it easier to read and understand.

##### Maximum Line Length

Limit lines to a maximum of 120 characters. For long lines, follow these wrapping guidelines:

1. Place the first argument on a new line.
2. Use a single indentation level.
3. Place each argument on its own line.
4. Place the closing element on a new line.

**Function Calls**

**✅ Yes:**

```solidity
thisFunctionCallIsReallyLong(
    longArgument1,
    longArgument2,
    longArgument3
);
```

**❌ No:**

```solidity
thisFunctionCallIsReallyLong(longArgument1,
                              longArgument2,
                              longArgument3
);

thisFunctionCallIsReallyLong(longArgument1,
    longArgument2,
    longArgument3
);

thisFunctionCallIsReallyLong(
    longArgument1, longArgument2,
    longArgument3
);

thisFunctionCallIsReallyLong(
longArgument1,
longArgument2,
longArgument3
);

thisFunctionCallIsReallyLong(
    longArgument1,
    longArgument2,
    longArgument3);
```

**Assignment Statements**

**✅ Yes:**

```solidity
thisIsALongNestedMapping[being][set][toSomeValue] = someFunction(
    argument1,
    argument2,
    argument3,
    argument4
);
```

**❌ No:**

```solidity
thisIsALongNestedMapping[being][set][toSomeValue] = someFunction(argument1,
                                                                   argument2,
                                                                   argument3,
                                                                   argument4);
```

**Event Definitions and Event Emitters**

**✅ Yes:**

```solidity
event LongAndLotsOfArgs(
    address sender,
    address recipient,
    uint256 publicKey,
    uint256 amount,
    bytes32[] options
);

emit LongAndLotsOfArgs(
    sender,
    recipient,
    publicKey,
    amount,
    options
);
```

**❌ No:**

```solidity
event LongAndLotsOfArgs(address sender,
                        address recipient,
                        uint256 publicKey,
                        uint256 amount,
                        bytes32[] options);

emit LongAndLotsOfArgs(sender,
                  recipient,
                  publicKey,
                  amount,
                  options);
```

> [!CAUTION]
> 🚨 Long lines can be difficult to read and understand. Breaking them up improves clarity.

##### Source File Encoding

Use UTF-8 or ASCII encoding for Solidity files.

> [!NOTE]
> Consistent file encoding ensures compatibility and prevents encoding-related issues across different environments and tools.

> [!TIP]
> 💡 UTF-8 should be preferred over ASCII as it supports a wider range of characters.

#### Use the Latest Version of Solidity

**Rule:** Always use the latest stable version of Solidity. This version includes the most recent fixes, gas optimizations, and security improvements, ensuring your smart contracts are up-to-date with the best practices and latest advancements. This recommendation comes directly from the maintainers of the Solidity repository, who are responsible for the ongoing development and improvement of the language. While some tools like Slither might suggest using older versions, using the latest version is crucial for maximizing security and performance.

> [!TIP]
> 💡 Regularly check for updates and migrate your code to the latest stable version to take advantage of new features and enhancements in Solidity.

#### Imports

Import statements should always be placed at the top of the file.

**A. Placing Imports**

Organize imports clearly at the top of the file to make dependencies easier to manage and understand.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract A {
    // ...
}

contract B is Owned {
    // ...
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
    // ...
}

import "./Owned.sol";

contract B is Owned {
    // ...
}
```

> [!NOTE]
> Organizing imports clearly at the top of the file makes dependencies easier to manage and understand.

**B. Use Named Imports**

Named imports or Selective Imports help readers understand what is being used and where it is declared.

**✅ Yes:**

```solidity
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
```

**❌ No:**

```solidity
import "@openzeppelin/contracts/access/Ownable.sol";
```

> [!NOTE]
> Named imports provide clarity on what is being imported, reducing potential confusion and making code review easier.

**C. Order Imports by Path Length**

Order imports by the length of their paths, from shortest to longest, to maintain a clean and organized structure.

**✅ Yes:**

```solidity
import {Math} from "./Math.sol";

import {Ownable} from "../access/Ownable.sol";
import {ERC20} from "../../token/ERC20.sol";
```

**❌ No:**

```solidity
import {Ownable} from "../access/Ownable.sol";
import {ERC20} from "../../token/ERC20.sol";
import {Math} from "./Math.sol";
```

> [!TIP]
> 💡 Ordering imports by path length improves readability by maintaining a consistent structure, making it easier to locate and manage dependencies.

**D. Group Imports by External and Internal**

Separate external and internal imports with a blank line and sort each group by path length.

**✅ Yes:**

```solidity
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {SafeMath} from "@openzeppelin/contracts/math/SafeMath.sol";

import {Math} from "./Math.sol";
import {MyHelper} from "./helpers/MyHelper.sol";
```

**❌ No:**

```solidity
import {Math} from "./Math.sol";
import {MyHelper} from "./helpers/MyHelper.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {SafeMath} from "@openzeppelin/contracts/math/SafeMath.sol";
```

> [!TIP]
> 💡 Grouping and sorting imports by their origin (external vs. internal) and path length keeps the codebase clean and well-organized, facilitating easier dependency management.

### Code Structure

#### Code Layout

Maintain a consistent code layout to improve readability and organization. Structure your code with clear separations between different sections and use proper indentation and spacing.

> [!TIP]
> 💡 A well-organized layout helps developers quickly understand the structure and flow of the code.

#### Order of Functions

Ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier.

Functions should be grouped according to their visibility and ordered:

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private

Within a grouping, place the `view` and `pure` functions last.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract A {
    constructor() {
        // ...
    }

    receive() external payable {
        // ...
    }

    fallback() external {
        // ...
    }

    // External functions
    // ...

    // External functions that are view
    // ...

    // External functions that are pure
    // ...

    // Public functions
    // ...

    // Internal functions
    // ...

    // Private functions
    // ...
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract A {

    // External functions
    // ...

    fallback() external {
        // ...
    }
    receive() external payable {
        // ...
    }

    // Private functions
    // ...

    // Public functions
    // ...

    constructor() {
        // ...
    }

    // Internal functions
    // ...
}
```

> [!TIP]
> 💡 Grouping functions by visibility and type helps maintain a clear and organized contract structure.

#### Order of Layout Elements

Arrange elements in the following order within contracts, libraries, or interfaces:

1. Pragma statements
2. Import statements
3. Events
4. Errors
5. Interfaces
6. Libraries
7. Contracts

> [!NOTE]
> This ordering helps readers identify the structure and dependencies of the code more easily.

Inside each contract, library, or interface, use the following order:

1. Type declarations
2. State variables
3. Events
4. Errors
5. Modifiers
6. Functions

> [!NOTE]
> It might be clearer to declare types close to their use in events or state variables.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.4 <0.9.0;

abstract contract Math {
    error DivideByZero();
    function divide(int256 numerator, int256 denominator) public virtual returns (uint256);
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.4 <0.9.0;

abstract contract Math {
    function divide(int256 numerator, int256 denominator) public virtual returns (uint256);
    error DivideByZero();
}
```

#### Single Contract or Interface Per File

Each Solidity file should contain only one contract or interface to simplify navigation and improve readability.

> [!TIP]
> 💡 Keeping a single contract or interface per file enhances maintainability and reduces complexity.

### Naming Conventions

Naming conventions are powerful when adopted and used broadly. The use of different conventions can convey significant _meta_ information that would otherwise not be immediately available.

The naming recommendations given here are intended to improve readability, and thus they are not rules, but rather guidelines to try and help convey the most information through the names of things.

Lastly, consistency within a codebase should always supersede any conventions outlined in this document.

#### Naming Styles

Use consistent naming styles to convey the purpose and scope of variables and functions:

- `b` (single lowercase letter)
- `B` (single uppercase letter)
- `lowercase`
- `UPPERCASE`
- `SNAKE_UPPER_CASE`
- `PascalCase`
- `camelCase`

> [!NOTE]
> Consistent naming styles improve readability and help convey meta-information.

> [!NOTE]
> When using initialisms in PascalCase, capitalize all the letters of the initialisms. Thus `HTTPServerError` is better than `HttpServerError`. When using initialisms in camelCase, capitalize all the letters of the initialisms, except keep the first one lowercase if it is the beginning of the name. Thus `xmlHTTPRequest` is better than `XMLHTTPRequest`.

#### Names to Avoid

Avoid using names that are easily confused with each other or with numerals, such as `l`, `O`, and `I`.

> [!NOTE]
> Using ambiguous names can lead to confusion and errors.

> [!CAUTION]
> 🚨 Never use any of these for single letter variable names. They are often indistinguishable from the numerals one and zero.

#### Contract and Library Names

- Contracts and libraries should be named using the PascalCase style. Examples: `SimpleToken`, `SmartBank`, `CertificateHashRepository`, `Player`, `Congress`, `Owned`.
- Contract and library names should also match their filenames.
- If a contract file includes multiple contracts and/or libraries, then the filename should match the _core contract_. This is not recommended however if it can be avoided.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// Owned.sol
contract Owned {
    address public owner;

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function transferOwnership(address newOwner) public onlyOwner {
        owner = newOwner;
    }
}
```

and in `Congress.sol`:

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract Congress is Owned, TokenRecipient {
    //...
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// owned.sol
contract owned {
    address public owner;

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function transferOwnership(address newOwner) public onlyOwner {
        owner = newOwner;
    }
}
```

and in `Congress.sol`:

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.7.0;

import "./owned.sol";

contract Congress is owned, tokenRecipient {
    //...
}
```

> [!TIP]
> 💡 Clear and consistent naming of contracts and libraries aids in project organization and readability.

#### Naming Interfaces

**Rule:** Interfaces should be named in a way that starts with `I` followed by the name of the contract it interfaces for, or you can use `ContractNameInterface`. Whichever naming convention you choose, you should stick to it.

> [!NOTE]
> Consistent naming of interfaces improves readability and helps in distinguishing between contracts and interfaces. This practice makes the code more intuitive and easier to navigate, especially in larger codebases.

**Example:**

**✅ Yes:**

```solidity
interface IToken {
    function transfer(address recipient, uint256 amount) external returns (bool);
}
```

or

```solidity
interface TokenInterface {
    function transfer(address recipient, uint256 amount) external returns (bool);
}
```

**❌ No:**

```solidity
interface token {
    function transfer(address recipient, uint256 amount) external returns (bool);
}
```

#### Defining Contract Types in Interfaces

**Rule:** Define all events, errors, structs, and optionally function names within interfaces for better modular organization and clarity.

> [!TIP]
> 💡 Grouping related types within interfaces enhances modularity and clarity, making it easier to manage and understand the structure of contracts.

**Example:**

**✅ Yes:**

```solidity
interface IToken {
    struct TokenData {
        address issuer;
        uint256 value;
    }
    error Unauthorized();
    event TokenIssued(address indexed issuer, uint256 value);
}

// Usage in contract
contract Token is IToken {
    // Implementation details
}
```

**❌ No:**

```solidity
contract Token {
    struct TokenData {
        address issuer;
        uint256 value;
    }
    error Unauthorized();
    event TokenIssued(address indexed issuer, uint256 value);
}
```

#### Struct Names

Structs should be named using PascalCase to distinguish them from variables and functions.

Examples: `MyCoin`, `Position`, `PositionXY`.

#### Event Names

Events should be named using PascalCase and should convey the past tense of an action.
Examples: `ContractUpgraded`, `FundsDeposited`.`TransferCompleted`.

> [!NOTE]
> Clear event names improve the understanding of emitted logs.

#### Function Names

Functions should use camelCase. Examples: `getBalance`, `transfer`, `verifyOwner`, `addMember`, `changeOwner`.

#### Variable Names

Variable names should use camelCase and be descriptive to convey their purpose.

Examples: `totalSupply`, `remainingSupply`, `balancesOf`, `creatorAddress`, `isPreSale`, `tokenExchangeRate`.

> [!TIP]
> 💡 Descriptive names help in understanding the code without needing extensive comments.

#### Function Argument Names

Function arguments should use camelCase. Examples: `initialSupply`, `account`, `recipientAddress`, `senderAddress`, `newOwner`.

When writing library functions that operate on a custom struct, the struct should be the first argument and should always be named `self`.

#### Constants

Name constants using all uppercase letters with underscores separating words, e.g., `MAX_SUPPLY`. If a constant is private, prefix it with an underscore.

Examples of public constants:

- `MAX_BLOCKS`
- `TOKEN_NAME`
- `TOKEN_TICKER`
- `CONTRACT_VERSION`

Examples of private constants:

- `_MAX_BLOCKS`
- `_TOKEN_NAME`
- `_TOKEN_TICKER`
- `_CONTRACT_VERSION`

> [!IMPORTANT]
> Consistent naming of constants using **SNAKE_UPPER_CASE** helps in quickly identifying them and prevents accidental modification. This practice enhances code readability and maintainability.

> [!TIP]
> 💡 Prefixing private constants with an underscore `_` clarifies their visibility and scope, aiding in code organization and readability.

#### Modifier Names

Modifiers should use camelCase and clearly describe the condition they enforce, e.g., `onlyOwner`.

#### Enums

Enums should be named using PascalCase and clearly describe their purpose, e.g., `UserRole`.

#### Avoiding Naming Collisions

Use a single trailing underscore to avoid naming collisions with existing variables, functions, or reserved keywords, e.g., `variable_`.

> [!NOTE]
> Avoiding naming collisions reduces confusion and potential errors.

> [!TIP]
> 💡 Trailing underscores should be used primarily for parameters or variables that might otherwise collide with reserved keywords, functions, or other variables.

#### Underscore Prefix for Non-external Functions and Variables

Prefix non-external functions and variables with a single underscore to indicate they are internal or private, e.g., `_internalFunction`.

> [!IMPORTANT]
> Using an underscore prefix helps differentiate internal/private functions and variables from external ones, improving code clarity.

- **\_singleLeadingUnderscore**: This convention is used for non-external functions and state variables (`private` or `internal`). State variables without specified visibility are `internal` by default.

When designing a smart contract, consider the public-facing API (functions callable by any account). Leading underscores help recognize the intent of non-external functions and variables. If you change a function from non-external to external (including `public`) and rename it, this forces a review of every call site, helping prevent unintended external functions and common security vulnerabilities.

> [!TIP]
> 💡 These conventions aim to create a consistent and readable codebase, making it easier to maintain and understand.

### Code Formatting

#### Whitespace in Expressions

Avoid extraneous whitespace in the following situations:

Immediately inside parentheses, brackets, or braces, with the exception of single-line function declarations.

**✅ Yes:**

```solidity
spam(ham[1], Coin({name: "ham"}));
```

**❌ No:**

```solidity
spam( ham[ 1 ], Coin( { name: "ham" } ) );
```

Exception:

```solidity
function singleLine() public { spam(); }
```

Immediately before a comma, semicolon:

**✅ Yes:**

```solidity
function spam(uint i, Coin coin) public;
```

**❌ No:**

```solidity
function spam(uint i , Coin coin) public ;
```

More than one space around an assignment or other operator to align with another:

**✅ Yes:**

```solidity
x = 1;
y = 2;
longVariable = 3;
```

**❌ No:**

```solidity
x            = 1;
y            = 2;
longVariable = 3;
```

Do not include whitespace in the receive and fallback functions:

**✅ Yes:**

```solidity
receive() external payable {
    ...
}

fallback() external {
    ...
}
```

**❌ No:**

```solidity
receive () external payable {
    ...
}

fallback () external {
    ...
}
```

> [!IMPORTANT]
> Avoiding unnecessary whitespace in expressions helps maintain clean and readable code.

#### Control Structures

- Place the opening brace `{` on the same line as the control structure.
- Close the brace `}` on its own line.
- Use a single space between the control structure keyword and the parenthesis.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Coin {
    struct Bank {
        address owner;
        uint balance;
    }
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Coin
{
    struct Bank {
        address owner;
        uint balance;
    }
}
```

The same recommendations apply to the control structures `if`, `else`, `while`, and `for`.

Additionally, there should be a single space between the control structures `if`, `while`, and `for` and the parenthetic block representing the conditional, as well as a single space between the conditional parenthetic block and the opening brace.

**✅ Yes:**

```solidity
if (...) {
    ...
}

for (...) {
    ...
}
```

**❌ No:**

```solidity
if (...)
{
    ...
}

while(...){
}

for (...) {
    ...;}
```

For control structures whose body contains a single statement, omitting the braces is okay _if_ the statement is contained on a single line.

**✅ Yes:**

```solidity
if (x < 10)
    x += 1;
```

**❌ No:**

```solidity
if (x < 10)
    someArray.push(Coin({
        name: 'spam',
        value: 42
    }));
```

For `if` blocks that have an `else` or `else if` clause, the `else` should be placed on the same line as the `if`'s closing brace. This is an exception compared to the rules of other block-like structures.

**✅ Yes:**

```solidity
if (x < 3) {
    x += 1;
} else if (x > 7) {
    x -= 1;
} else {
    x = 5;
}

if (x < 3)
    x += 1;
else
    x -= 1;
```

**❌ No:**

```solidity
if (x < 3) {
    x += 1;
}
else {
    x -= 1;
}
```

> [!TIP]
> 💡 Consistent formatting of control structures improves readability and helps prevent errors.

#### Function Declarations

- For short functions, place the opening brace on the same line as the declaration.
- For long functions, break each parameter onto a new line.
- Use the order: visibility, mutability, virtual, override, and custom modifiers.

**✅ Yes:**

```solidity
function increment(uint x) public pure returns (uint) {
    return x + 1;
}

function increment(uint x) public pure onlyOwner returns (uint) {
    return x + 1;
}
```

**❌ No:**

```solidity
function increment(uint x) public pure returns (uint)
{
    return x + 1;
}

function increment(uint x) public pure returns (uint){
    return x + 1;
}

function increment(uint x) public pure returns (uint) {
    return x + 1;
    }

function increment(uint x) public pure returns (uint) {
    return x + 1;}
```

The modifier order for a function should be:

1. Visibility
2. Mutability
3. Virtual
4. Override
5. Custom modifiers

**✅ Yes:**

```solidity
function balance(uint from) public view override returns (uint) {
    return balanceOf[from];
}

function increment(uint x) public pure onlyOwner returns (uint) {
    return x + 1;
}
```

**❌ No:**

```solidity
function balance(uint from) public override view returns (uint) {
    return balanceOf[from];
}

function increment(uint x) onlyOwner public pure returns (uint) {
    return x + 1;
}
```

For long function declarations, it is recommended to drop each argument onto its own line at the same indentation level as the function body. The closing parenthesis and opening bracket should be placed on their own line as well at the same indentation level as the function declaration.

**✅ Yes:**

```solidity
function thisFunctionHasLotsOfArguments(
    address a,
    address b,
    address c,
    address d,
    address e,
    address f
)
    public
{
    doSomething();
}
```

**❌ No:**

```solidity
function thisFunctionHasLotsOfArguments(address a, address b, address c,
    address d, address e, address f) public {
    doSomething();
}

function thisFunctionHasLotsOfArguments(address a,
                                        address b,
                                        address c,
                                        address d,
                                        address e,
                                        address f) public {
    doSomething();
}

function thisFunctionHasLotsOfArguments(
    address a,
    address b,
    address c,
    address d,
    address e,
    address f) public {
    doSomething();
}
```

If a long function declaration has modifiers, then each modifier should be dropped to its own line.

**✅ Yes:**

```solidity
function thisFunctionNameIsReallyLong(address x, address y, address z)
    public
    onlyOwner
    priced
    returns (address)
{
    doSomething();
}

function thisFunctionNameIsReallyLong(
    address x,
    address y,
    address z
)
    public
    onlyOwner
    priced
    returns (address)
{
    doSomething();
}
```

**❌ No:**

```solidity
function thisFunctionNameIsReallyLong(address x, address y, address z)
                                      public
                                      onlyOwner
                                      priced
                                      returns (address) {
    doSomething();
}

function thisFunctionNameIsReallyLong(address x, address y, address z)
    public onlyOwner priced returns (address)
{
    doSomething();
}

function thisFunctionNameIsReallyLong(address x, address y, address z)
    public
    onlyOwner
    priced
    returns (address) {
    doSomething();
}
```

Multiline output parameters and return statements should follow the same style recommended for wrapping long lines found in the maximum line length section.

**✅ Yes:**

```solidity
function thisFunctionNameIsReallyLong(
    address a,
    address b,
    address c
)
    public
    returns (
        address someAddressName,
        uint256 LongArgument,
        uint256 Argument
    )
{
    doSomething();

    return (
        veryLongReturnArg1,
        veryLongReturnArg2,
        veryLongReturnArg3
    );
}
```

**❌ No:**

```solidity
function thisFunctionNameIsReallyLong(
    address a,
    address b,
    address c
)
    public
    returns (address someAddressName,
             uint256 LongArgument,
             uint256 Argument)
{
    doSomething();

    return (veryLongReturnArg1,
            veryLongReturnArg1,
            veryLongReturnArg1);
}
```

For constructor functions on inherited contracts whose bases require arguments, it is recommended to drop the base constructors onto new lines in the same manner as modifiers if the function declaration is long or hard to read.

**✅ Yes:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// Base contracts just to make this compile
contract B {
    constructor(uint) {}
}

contract C {
    constructor(uint, uint) {}
}

contract D {
    constructor(uint) {}
}

contract A is B, C, D {
    uint x;

    constructor(uint param1, uint param2, uint param3, uint param4, uint param5)
        B(param1)
        C(param2, param3)
        D(param4)
    {
        // do something with param5
        x = param5;
    }
}
```

**❌ No:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// Base contracts just to make this compile
contract B {
    constructor(uint) {}
}

contract C {
    constructor(uint, uint) {}
}

contract D {
    constructor(uint) {}
}

contract A is B, C, D {
    uint x;

    constructor(uint param1, uint param2, uint param3, uint param4, uint param5)
    B(param1)
    C(param2, param3)
    D(param4) {
        x = param5;
    }
}

contract X is B, C, D {
    uint x;

    constructor(uint param1, uint param2, uint param3, uint param4, uint param5)
        B(param1)
        C(param2, param3)
        D(param4) {
            x = param5;
        }
}
```

When declaring short functions with a single statement, it is permissible to do it on a single line.

Permissible:

```solidity
function shortFunction() public { doSomething(); }
```

> [!TIP]
> 💡 These guidelines for function declarations are intended to improve readability. Authors should use their best judgment as this guide does not try to cover all possible permutations for function declarations.

#### Mappings

Do not separate the `mapping` keyword from its type with a space.

**✅ Yes:**

```solidity
mapping(uint => uint) map;
mapping(address => bool) registeredAddresses;
mapping(uint => mapping(bool => Data[])) public data;
mapping(uint => mapping(uint => s)) data;
```

**❌ No:**

```solidity
mapping (uint => uint) map;
mapping( address => bool ) registeredAddresses;
mapping (uint => mapping (bool => Data[])) public data;
mapping(uint => mapping (uint => s)) data;
```

> [!NOTE]
> Keeping `mapping` keywords without spaces ensures consistent formatting and readability.

#### Variable Declarations

Do not add a space between the type and the brackets for array variables.

**✅ Yes:**

```solidity
uint[] x;
```

**❌ No:**

```solidity
uint [] x;
```

> [!TIP]
> 💡 Consistent formatting of variable declarations helps in maintaining readability and avoids confusion.

> [!TIP]
> 💡 Consistent variable declarations prevent confusion and improve readability.

#### Strings

Strings should be quoted with double-quotes instead of single-quotes.

**✅ Yes:**

```solidity
string public greeting = "Hello, World!";
```

**❌ No:**

```solidity
string public greeting = 'Hello, World!';
```

> [!NOTE]
> Using double quotes for strings ensures consistency and aligns with common programming practices.

#### Operators

Surround operators with a single space on either side.

**✅ Yes:**

```solidity
x = 3;
x = 100 / 10;
x += 3 + 4;
x |= y && z;
```

**❌ No:**

```solidity
x=3;
x = 100/10;
x += 3+4;
x |= y&&z;
```

Operators with a higher priority than others can exclude surrounding whitespace in order to denote precedence. This is meant to allow for improved readability for complex statements. You should always use the same amount of whitespace on either side of an operator:

**✅ Yes:**

```solidity
x = 2**3 + 5;
x = 2*y + 3*z;
x = (a+b) * (a-b);
```

**❌ No:**

```solidity
x = 2** 3 + 5;
x = y+z;
x +=1;
```

> [!TIP]
> 💡 Consistent spacing around operators enhances readability and ensures that code is easy to understand.

### Documentation

#### NatSpec Documentation

Solidity contracts can also contain NatSpec comments. They are written with a triple slash (`///`) or a double asterisk block (`/** ... */`) and they should be used directly above function declarations or statements.

**Example:**

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

/// @author The Solidity Team
/// @title A simple storage example
contract SimpleStorage {
    uint storedData;

    /// Store `x`.
    /// @param x the new value to store
    /// @dev stores the number in the state variable `storedData`
    function set(uint x) public {
        storedData = x;
    }

    /// Return the stored value.
    /// @dev retrieves the value of the state variable `storedData`
    /// @return the stored value
    function get() public view returns (uint) {
        return storedData;
    }
}
```

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI).

> [!TIP]
> 💡 Proper documentation using NatSpec improves code maintainability and usability, especially for public APIs.

> [!NOTE]
> NatSpec should not be used only for public interfaces but also for any function that might be used by other developers, including internal APIs (functions).

### Best Practices

#### Using Custom Errors Over Require

**Rule:** Utilize custom errors instead of `require` statements for clearer and more gas-efficient error handling. Solidity 0.8.26 supports the use of custom errors with `require`.

**Example:**

```solidity
error InsufficientFunds(uint256 requested, uint256 available);

function withdraw(uint256 amount) public {
    if (amount > balance) {
        revert InsufficientFunds(amount, balance);
    }
    balance -= amount;
}
```

> [!TIP]
> 💡 Custom errors save gas and provide more detailed error messages compared to traditional `require` strings.

#### Require with Custom Error (Solidity 0.8.26+)

**Rule:** Use the new `require(condition, error)` syntax to include custom errors in `require` statements, available in Solidity 0.8.26 and later.

**Example:**

```solidity
error InsufficientFunds(uint256 requested, uint256 available);

function withdraw(uint256 amount) public {
    require(amount <= balance, InsufficientFunds(amount, balance));
    balance -= amount;
}
```

> [!IMPORTANT]
> This new syntax provides a more efficient way to handle errors directly within `require` statements, enhancing both readability and gas efficiency.

#### Limit Require Messages

**Rule:** Prefer using custom errors over `require` with strings for better efficiency. If you must use `require` with a string message, keep it under 32 bytes to reduce gas costs.

> [!IMPORTANT]
> Custom errors are more gas-efficient and provide clearer error handling. Whenever possible, use them instead of `require` with a string message.

**✅ Yes:**

```solidity
require(balance >= amount, "Insufficient funds");
```

> [!CAUTION]
> 🚨 Keeping `require` messages concise (under 32 bytes) minimizes additional gas costs and improves efficiency.

**❌ No:**

```solidity
require(balance >= amount, "The balance is insufficient for the withdrawal amount requested.");
```

> [!WARNING]
> ⚠️ Longer messages significantly increase gas costs. Avoid using verbose messages in `require` statements.

#### Calldata for Read-Only Function Parameters

**Rule:** Using calldata can significantly reduce gas costs for external functions. It is beneficial for any external function, not just view functions, as long as the parameters are read-only.

**✅ Yes:**

```solidity
function totalBalance(address[] calldata accounts) external view returns (uint256 total) {
    for (uint i = 0; i < accounts.length; i++) {
        total += balances[accounts[i]];
    }
}
```

**❌ No:**

```solidity
function totalBalance(address[] memory accounts) external view returns (uint256 total) {
    for (uint i = 0; i < accounts.length; i++) {
        total += balances[accounts[i]];
    }
}
```

> [!TIP]
> 💡 Using `calldata` can significantly reduce gas costs for external functions. It is beneficial for any external function, not just view functions, as long as the parameters are read-only.

#### Optimize Length in Loops

**Rule:** Cache the length of arrays when used in loop conditions to minimize gas cost.

**✅ Yes:**

```solidity
uint length = myArray.length;
for (uint i = 0; i < length; i++) {
    // Some logic
}
```

**❌ No:**

```solidity
for (uint i = 0; i < myArray.length; i++) {
    // Some logic
}
```

> [!CAUTION]
> 🚨 Accessing array length multiple times in a loop increases gas costs. Caching the length improves efficiency.

#### Prefer Named Return

**Rule:** Use named return arguments for gas efficiency and clarity, especially in functions with multiple return values.

**✅ Yes:**

```solidity
function calculate(uint256 a, uint256 b) public pure returns (uint256 sum, uint256 product) {
    sum = a + b;
    product = a * b;
}
```

**❌ No:**

```solidity
function calculate(uint256 a, uint256 b) public pure returns (uint256, uint256) {
    uint256 sum = a + b;
    uint256 product = a * b;
    return (sum, product);
}
```

> [!TIP]
> 💡 Named return variables save gas by avoiding redundant return statements and make the code more readable.

#### Prefer Named Arguments

**Rule:** Use named arguments for function calls, events, and errors to improve clarity.

**Example:**

**✅ Yes:**

```solidity
pow({base: x, exponent: y, scalar: v});
```

**❌ No:**

```solidity
pow(x, y, v);
```

> [!IMPORTANT]
> Explicitly naming arguments improves readability and reduces the chance of errors.

#### Prefer Named Parameters in Mapping Types

**Rule:** Explicitly name parameters in mapping types for clarity, especially when nesting is used.

**✅ Yes:**

```solidity
mapping(address account => mapping(address asset => uint256 amount)) public balances;
```

**❌ No:**

```solidity
mapping(uint256 => mapping(address => uint256)) public balances;
```

> [!TIP]
> 💡 Named parameters in mappings make the purpose and usage of the mappings clearer.

#### Enforcing Explicit Types

**Rule:** Always declare explicit types for all variable and function return declarations. Avoid using ambiguous types.

**✅ Yes:**

```solidity
uint256 public balance;
function getBalance() external view returns (uint256) {}
```

**❌ No:**

```solidity
uint balance = 256;  // Use explicit uint256
function getBalance() external view returns (uint) {}  // Use explicit uint256
```

> [!TIP]
> 💡 Using explicit types prevents ambiguity and ensures clarity in your code.

#### Internal Function Naming

**Rule:** Internal functions in a library should not have an underscore prefix.

**Example:**

**✅ Yes:**

```solidity
library MathLib {
    function add(uint256 a, uint256 b) internal pure returns (uint) {
        return a + b;
    }
}

using MathLib for uint256;
uint256 result = x.add(y);
```

**❌ No:**

```solidity
library MathLib {
    function _add(uint a, uint b) internal pure returns (uint) {
        return a + b;
    }
}

using MathLib for uint;
uint256 result = x._add(y);
```

> [!IMPORTANT]
> Internal functions within libraries should be easy to read and follow, avoiding unnecessary prefixes.

#### Contract Interactions Through Interfaces

**Rule:** Whenever possible, interact with external contracts through well-defined interfaces. Direct contract calls should be avoided unless they offer specific benefits. If using `call`, prefer `abi.encodeWithSelector` to avoid issues.

> [!IMPORTANT]
> Using interfaces for external contract interactions enhances security by ensuring that only defined and expected methods are called, reducing the risk of unexpected behavior. This approach also makes the code more modular and easier to test.

**Example:**

**✅ Yes:**

```solidity
interface IERC20 {
    function transfer(address recipient, uint256 amount) external returns (bool);
}

contract MyContract {
    IERC20 private _token;

    constructor(address tokenAddress) {
        _token = IERC20(tokenAddress);
    }

    function transferToken(address recipient, uint256 amount) public {
        _token.transfer(recipient, amount);
    }
}
```

**❌ No:**

```solidity
contract MyContract {
    address private _tokenAddress;

    function transferToken(address recipient, uint256 amount) public {
        (bool success, ) = _tokenAddress.call(abi.encodeWithSignature("transfer(address,uint256)", recipient, amount));
        require(success, "Transfer failed.");
    }
}
```

**Better Approach:**

```solidity
contract MyContract {
    address private _tokenAddress;

    function transferToken(address recipient, uint256 amount) public {
        (bool success, ) = _tokenAddress.call(abi.encodeWithSelector(IERC20.transfer.selector, recipient, amount));
        require(success, "Transfer failed.");
    }
}
```

#### Errors

**Rule:** Prefer custom errors over traditional error messages for better efficiency and clarity.

**Naming Convention:** Custom error names should follow PascalCase.

**Example:**

```solidity
error InsufficientBalance(uint256 requested, uint256 available);
```

> [!TIP]
> 💡 Use custom errors to save gas and make error handling more descriptive.

#### Events

**Rule:** Event names should be in past tense and follow the `SubjectVerb` format.

**Example:**

**✅ Yes:**

```solidity
event OwnerUpdated(address newOwner);
```

**❌ No:**

```solidity
event OwnerUpdate(address newOwner);
event UpdatedOwner(address newOwner);
```

> [!NOTE]
> Consistent event naming helps understand contract behavior by reading the emitted events.

#### Struct, Event and Error Definitions

**Rule:** Declare structs, events and errors within their scope. If a struct or error is used across many files, define them in their own file. Multiple structs and errors can be defined together in one file.

> [!TIP]
> 💡 Centralize common structures, events and errors to improve maintainability and clarity.

#### Upgradability

**Rule:** Prefer the [ERC-7201](https://eips.ethereum.org/EIPS/eip-7201) "Namespaced Storage Layout" convention to avoid storage collisions.

#### Avoid Unnecessary Version Pragma Constraints

**Rule:** Avoid unnecessary version pragma constraints. While main contracts should specify a single Solidity version, supporting contracts and libraries should have as open a pragma as possible.

**✅ Yes:**

```solidity
pragma solidity ^0.8.0;
```

**❌ No:**

```solidity
pragma solidity ^0.8.0 ^0.9.0;
```

> [!TIP]
> 💡 Use open pragmas for supporting contracts and libraries to enhance compatibility and flexibility.

#### Avoid Using Assembly

**Rule:** Use inline assembly with extreme care. Ensure that it is well-documented with inline comments explaining what the assembly code does. Avoid using assembly unless it adds significant value and there are no better alternatives.

**Example:**

```solidity
function add(uint x, uint y) public pure returns (uint result) {
    assembly {
        // Add x and y and store the result in the `result` variable
        result := add(x, y)
    }
}
```

> [!WARNING]
> ⚠️ Assembly code is hard to read and audit, increasing the risk of errors and vulnerabilities. Use it only when necessary and ensure thorough documentation to maintain code clarity and security.

> [!CAUTION]
> 🚨 Avoid using assembly if it does not provide significant performance or functional benefits. Always prefer high-level Solidity when possible.

#### Prefer Composition Over Inheritance

**Rule:** Prefer defining functions as part of a larger contract rather than creating many small contracts.

> [!NOTE]
> Inheritance is useful but should be used judiciously, especially when building on existing, trusted contracts like `Ownable` from OpenZeppelin.

These best practices help ensure that Solidity code is secure, efficient, and maintainable, leveraging the latest features and conventions of Solidity 0.8.26.

### Testing (Foundry Specific)

#### Test Structure

Foundry provides a flexible and efficient framework for structuring your tests. Here are the recommended structures:

- **Unit Tests**

  - Organize by contract or functionality:
    - Treat contracts as describe blocks: e.g., `contract Add`, `contract Supply`.
    - Have a test contract per contract-under-test: e.g., `contract MyContractTest`.
  - **Example:**

  ```solidity
  contract Add {
      function test_add_AddsTwoNumbers() public {
          // Test code
      }
  }

  contract MyContractTest {
      function test_add_AddsTwoNumbers() public {
          // Test code
      }

      function test_supply_UsersCanSupplyTokens() public {
          // Test code
      }
  }
  ```

- **Integration Tests**
  - Place in the same test directory.
  - Clear naming convention to distinguish from unit tests.

> [!TIP]
> 💡 Organizing tests logically improves maintainability and makes it easier to identify and fix issues.

#### Unit Tests

- **Test Coverage**

  - Ensure all functionalities are covered.
  - Use `test_Description` for standard tests.
  - Use `testFuzz_Description` for fuzz tests.
  - Example:

  ```solidity
  function test_transfer() public {
      // Test code
  }

  function testFuzz_transfer(uint amount) public {
      // Test code
  }
  ```

- **Test Naming Conventions**

  - Consistent naming helps in filtering and identifying tests quickly.
  - Example:

  ```solidity
  function test_RevertIf_Condition() public {
      // Test code expecting revert
  }

  function testForkFuzz_RevertIf_Condition() public {
      // Fuzz test with fork expecting revert
  }
  ```

> [!NOTE]
> Consistent naming aids in test management and improves readability.

#### Test Fixtures

- Use fixtures to set up common test scenarios.
- Avoid making assertions in the `setUp` function. Instead, use a dedicated test like `test_SetUpState`.

> [!IMPORTANT]
> Isolating setup logic from assertions ensures clarity and reduces potential errors.

#### Mocking and Stubbing

- Utilize mocking and stubbing to simulate complex interactions and dependencies.
- Example:

  ```solidity
  contract MockContract {
      function mockedFunction() public returns (bool) {
          return true;
      }
  }
  ```

> [!TIP]
> 💡 Mocking and stubbing help in testing functionalities in isolation.

#### Property-Based Testing

- Foundry supports property-based testing to ensure that your contracts hold certain properties over a wide range of inputs.
- Example:

  ```solidity
  function test_property(uint x) public {
      assert(x < 1000);
  }
  ```

#### Gas Usage Testing

- Monitor and optimize gas usage by incorporating gas usage tests.
- Example:

  ```solidity
  function testGasUsage() public {
      uint gasStart = gasleft();
      // Function call
      uint gasUsed = gasStart - gasleft();
      emit log_named_uint("Gas used: ", gasUsed);
  }
  ```

> [!CAUTION]
> 🚨 Regular gas usage tests help in optimizing smart contract efficiency.

#### Foundry Tools and Utilities

- **Fuzz Testing**

  - Foundry's fuzz testing tools help in identifying edge cases and potential issues.
  - Example:

  ```solidity
  function testFuzz(uint x) public {
      // Fuzz test code
  }
  ```

- **Debugging with Foundry**

  - Utilize Foundry's debugging tools to trace and fix issues.
  - Example:

  ```solidity
  function testDebug() public {
      // Debug test code
  }
  ```

> [!TIP]
> 💡 Leveraging Foundry's tools and utilities enhances test coverage and debugging capabilities.

#### General Test Guidance

- **File Naming**: For `MyContract.sol`, the test file should be `MyContract.t.sol`.
- **Splitting Large Contracts**: Group logically, e.g., `MyContract.owner.t.sol`, `MyContract.deposits.t.sol`.
- **Assertions**: Avoid assertions in `setUp`; use dedicated tests.
- **Test Contracts**: Organize unit tests logically within contracts.

> [!NOTE]
> Consistent file naming and structure make it easier to locate and manage tests.

These practices and tools ensure comprehensive and efficient testing, leveraging Foundry's capabilities to maintain robust and reliable smart contracts.

### Performance and Security

#### Gas Optimization

Optimizing gas usage is crucial for efficient and cost-effective smart contracts. Here are some best practices:

- **Minimize Storage Operations**: Storage operations (SSTORE and SLOAD) are expensive. Minimize their usage by:
  - Caching storage variables in memory.
  - Using `calldata` for function parameters.
- **Use Immutable and Constant**: Mark variables as `immutable` or `constant` where possible to save gas.
- **Optimize Loops**: Cache array lengths and avoid unnecessary computations within loops.
- **Prefer `uint256`**: Using `uint256` over smaller types like `uint8` or `uint32` can be more gas efficient due to padding.

**Example:**

```solidity
uint immutable public value; // Immutable variable
uint[] public data;

function optimizedFunction(uint[] calldata input) external {
    uint length = input.length; // Cache array length
    for (uint i = 0; i < length; i++) {
        data.push(input[i]);
    }
}
```

#### Security Best Practices

Security is paramount in smart contract development. Adhere to the following best practices to mitigate common vulnerabilities:

##### Reentrancy

Reentrancy attacks occur when a contract calls an external contract before updating its state, allowing the external contract to call back into the original contract and manipulate its state. Prevent reentrancy by:

- **Using Checks-Effects-Interactions Pattern**: Perform all state changes before calling external contracts.
- **Reentrancy Guard**: Use a mutex or a reentrancy guard.

**Example:**

```solidity
bool private locked;

modifier noReentrant() {
    require(!locked, "Reentrant call");
    locked = true;
    _;
    locked = false;
}

function withdraw(uint amount) external noReentrant {
    require(balances[msg.sender] >= amount, "Insufficient balance");
    balances[msg.sender] -= amount;
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success, "Transfer failed");
}
```

> [!WARNING]
> ⚠️ Always perform state updates before calling external contracts to prevent reentrancy attacks.

##### Access Control

Ensure proper access control mechanisms are in place:

- **Use `onlyOwner` Modifiers**: Restrict critical functions to the contract owner or specific roles.
- **Role-Based Access Control**: Implement role-based access control (RBAC) for fine-grained permissions.

**Example:**

```solidity
address public owner;
mapping(address => bool) public admins;

modifier onlyOwner() {
    require(msg.sender == owner, "Not owner");
    _;
}

modifier onlyAdmin() {
    require(admins[msg.sender], "Not admin");
    _;
}

function addAdmin(address admin) external onlyOwner {
    admins[admin] = true;
}
```

> [!TIP]
> 💡 Use libraries like OpenZeppelin's Access Control for robust access management.

##### Integer Overflow and Underflow

Prevent integer overflow and underflow by:

- **Using SafeMath Library**: Use OpenZeppelin's `SafeMath` library for safe arithmetic operations.
- **Solidity 0.8+**: Solidity 0.8 and later versions have built-in overflow and underflow checks.

**Example:**

```solidity
using SafeMath for uint256;

function safeAdd(uint256 a, uint256 b) public pure returns (uint256) {
    return a.add(b);
}
```

> [!CAUTION]
> 🚨 Always use safe arithmetic operations to prevent unexpected overflows and underflows.

##### Handling Ether Transfers

Handle Ether transfers securely by:

- **Using `call` instead of `transfer` or `send`**: `call` provides more flexibility and forwards all available gas.
- **Check Transfer Success**: Always check the return value of `call`.

**Example:**

```solidity
function safeTransfer(address payable recipient, uint256 amount) internal {
    (bool success, ) = recipient.call{value: amount}("");
    require(success, "Transfer failed");
}
```

> [!IMPORTANT]
> Properly handle Ether transfers to avoid vulnerabilities related to gas limits and failed transfers.

#### Code Reviews and Audits

Regular code reviews and security audits are essential for identifying and mitigating potential vulnerabilities:

- **Internal Code Reviews**: Conduct regular internal reviews to catch issues early.
- **External Audits**: Engage reputable auditing firms for comprehensive security audits.
- **Automated Tools**: Use automated security analysis tools like [MythX](https://mythx.io/) or [Slither](https://github.com/crytic/slither) to scan for vulnerabilities.

> [!TIP]
> 💡 Regularly update and audit your contracts, especially after significant changes or before deployment.

By following these best practices, you can enhance the performance, security, and robustness of your Solidity smart contracts.

### Conclusion

This Solidity Style Guide aims to enhance existing guidelines by providing additional, comprehensive information to ensure consistency, readability, and maintainability in your Solidity code. It draws inspiration from several valuable resources, which you can explore for further insights:

- [Solidity Official Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html)
- [Foundry Best Practices](https://book.getfoundry.sh/tutorials/best-practices)
- [RareSkills Solidity Style Guide](https://www.rareskills.io/post/solidity-style-guide)
- [Coinbase Solidity Style Guide](https://github.com/coinbase/solidity-style-guide/)

This guide is not intended to replace any existing style guides but to supplement them with additional best practices and recommendations.

Feel free to contribute or make suggestions to this guide. Any pull requests or contributions are welcomed to help us continually improve.

- [Twitter](https://twitter.com/adamboudj)
- [GitHub](https://github.com/Aboudjem)

Thank you for using this guide, and happy coding!
