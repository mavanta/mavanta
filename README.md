import random

class Shop:
    def __init__(self, player_money):
        self.items = {
            "Small Coin Pack": {"price": 100, "coins": 10},
            "Medium Coin Pack": {"price": 450, "coins": 50},
            "Large Coin Pack": {"price": 800, "coins": 100},
        }
        self.player_money = player_money
        self.player_coins = 0

    def display_items(self):
        print("Welcome to the Coin Shop!")
        for item, details in self.items.items():
            print(f"{item}: {details['price']} money, gives {details['coins']} coins")

    def buy_item(self, item_name):
        if item_name in self.items:
            item = self.items[item_name]
            if self.player_money >= item['price']:
                self.player_money -= item['price']
                self.player_coins += item['coins']
                print(f"You bought {item_name} and received {item['coins']} coins!")
            else:
                print("You don't have enough money to buy this item.")
        else:
            print("This item does not exist in the shop.")

    def get_status(self):
        print(f"Player Money: {self.player_money}")
        print(f"Player Coins: {self.player_coins}")

def main():
    player_money = 1000
    shop = Shop(player_money)

    while True:
        shop.display_items()
        print("\nType the name of the item you want to buy or type 'exit' to leave the shop.")
        choice = input("Your choice: ")

        if choice.lower() == 'exit':
            break

        shop.buy_item(choice)
        shop.get_status()

if __name__ == "__main__":
    main()


