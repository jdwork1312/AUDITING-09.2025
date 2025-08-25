Mental Attack Template

1. Map the State

Storage variables: [list variables touched]

Local variables: [intermediate calculations, temp storage]

Attacker check: Which can I influence? (directly or indirectly)

2. Map the Flow

Step through the function: [function calls, calculations, external calls]

Highlight critical state changes and external calls.

3. List Assumptions

[What the developer assumes is safe]

Ask: Can I break these assumptions?

4. Stress-Test / Edge Cases

Numbers: overflow, rounding, underflow

Ordering: multi-call, reentrancy

External: price oracles, ERC-20 hooks, aToken transfers

Access: who can call what

5. Attack Chains

Combine quirks from flow/assumptions to find possible exploitation sequences

Include temporary manipulations (flash loans, oracle changes)

6. Notes / Observations

Highlight safe points

Highlight potential risk points

Example 1: Partial Liquidation

1. State:

userConfig, collateralReserve, debtReserve, vars.userCollateralBalance

2. Flow:

_calculateAvailableCollateralToLiquidate → determines how much collateral can be seized

setUsingAsCollateral → may disable collateral flag

transferOnLiquidation → external call

3. Assumptions:

User’s balance is sufficient

Liquidation only triggers if health factor < 1

4. Stress-Test:

User balance very close to liquidation threshold → rounding issues

Oracle slightly off → triggers liquidation prematurely

5. Attack Chain:

Flash loan → borrow debt asset → trigger liquidation → repay flash loan

Exploit rounding → get slightly more collateral than debt repaid

Example 2: Oracle Manipulation Risk

1. State:

collateralReserve, debtReserve, priceOracle

2. Flow:

calculateUserAccountData → health factor depends on price

_calculateAvailableCollateralToLiquidate → uses price to compute collateral

3. Assumptions:

Oracle price is accurate

User cannot manipulate state directly

4. Stress-Test:

Temporary price spike/drop → liquidation possible for healthy user

Sequence multiple liquidations in the same block

5. Attack Chain:

Manipulate price → trigger liquidation → profit from collateral → revert oracle price
