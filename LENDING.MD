
## LIQUIDATION

### Liquidation Process

Check: HF < 1.0
CALC: Max liquidation amount (debt × close factor)
Repay: Liquidator pays portion of debt
Seize: Liquidator receives collateral + bonus
Update: Recalculate health factor

### Liquidation Priority

Highest Value Collateral: Usually seized first
Most Liquid Assets: Preferred for efficiency
Gas Optimization: Minimize transaction costs


- Collateral factor (75%) = max you can borrow
- Liquidation threshold (80%) = when liquidation triggers

### HF
- Health Factor = (Collateral × Liq Threshold) / Debt
- Example: (2000 × 0.8) / 1000 = 1.6

