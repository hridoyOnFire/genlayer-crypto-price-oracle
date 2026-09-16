# { "Depends": "py-genlayer:1jb45aa8ynh2a9c9xn3b7qqh8sm5q93hwfp7jqmwsfhh8jpz09h6" }
from genlayer import *

class CryptoPriceOracle(gl.Contract):
    asset_pair: str
    last_price: str

    def __init__(self, asset_pair: str):
        self.asset_pair = asset_pair
        self.last_price = "0.00"

    @gl.public.write
    def update_price(self) -> None:
        """
        Uses GenLayer's AI Consensus to fetch live web data for the target asset.
        """
        prompt = f"Search the internet and get the current price in USD for {self.asset_pair}. Reply ONLY with the numerical value (e.g., 2500.50)."
        
        # Executing web search prompt through GenLayer Consensus
        price_result = gl.exec_prompt(prompt).strip()
        self.last_price = price_result

    @gl.public.view
    def get_price_info(self) -> str:
        return f"Asset: {self.asset_pair} | Last Updated Price: ${self.last_price}"
        # 📉 GenLayer AI Cross-Chain Crypto Price Oracle

An Intelligent Smart Contract deployed on the **GenLayer Testnet** that serves as a decentralized real-time crypto price oracle.

## 🚀 Overview
Traditional smart contracts require complex external oracle networks (like Chainlink) to access real-world financial data. This project leverages GenLayer's built-in AI consensus to dynamically query live Web API/Search data directly on-chain.

## 🛠️ Key Features
- **Direct Web Access:** Queries real-time market data without third-party middleware.
- **Decentralized AI Consensus:** Multiple validators reach consensus on the fetched asset price before writing it to state.
- **Lightweight & Modular:** Can be configured for any cryptocurrency or token pair upon deployment.

## 📂 Tech Stack
- **Language:** Python
- **Runtime:** GenVM
- **Framework:** `py-genlayer`
