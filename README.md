
# 📊 Wallet Risk Scoring using Compound V2 Protocol

## ✅ Objective
To evaluate the risk profile of 100 Ethereum wallet addresses based on their on-chain activity using the Compound V2 lending protocol.

## 📥 Data Collection
We used [The Graph Protocol](https://thegraph.com/) to collect historical data from the Compound V2 subgraph, including:
- **Borrow Events**
- **Repay Events**
- **Liquidation Events**

API endpoint used: `https://api.thegraph.com/subgraphs/name/graphprotocol/compound-v2`

## ⚙️ Features Extracted
For each wallet, we extracted:
- `num_borrows`: Number of borrow transactions
- `num_repays`: Number of repay transactions
- `num_liquidations`: Number of times the wallet was involved in liquidation
- `inactivity_days`: Number of days since last activity (inferred from block timestamps)

## 🧠 Risk Scoring Logic
The risk score is a number between **0 and 1000**, calculated using:
- Positive contribution from: `repays`, `borrows`
- Negative contribution from: `liquidations`, `inactivity_days`

We used **Min-Max Normalization** to scale the features, then computed a weighted score:


score = (
0.3 * repays_scaled +
0.3 * borrows_scaled +
0.2 * (1 - liquidations_scaled) +
0.2 * (1 - inactivity_days_scaled)
) * 1000

## 📤 Output
The final result is a CSV file with:
| wallet_id | score |
|-----------|-------|
| 0xfaa0768bde629806739c3a4620656c5d26f44ef2 | 732 |

## 🧾 Usage
To reproduce:
1. Run the full pipeline in Google Colab.
2. Ensure your `Wallet id.xlsx` file is uploaded.
3. Download the `wallet_scores.csv` and `README.md` for GitHub.

---
