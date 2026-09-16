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
