---
title: "Building a Simple ATM System in Python: A Casual Walkthrough"
seoTitle: "Simple Python ATM System: Step-by-Step Guide"
seoDescription: "Learn to build a simple ATM system in Python with this casual walkthrough and code examples"
datePublished: Sun Jun 02 2024 20:15:22 GMT+0000 (Coordinated Universal Time)
cuid: clwxzedx000000amo57h5bjxh
slug: simple-atm-system-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717359060903/94337903-f4b1-4ff2-9661-c742ea8b605e.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1717359292442/d3623569-e9bc-44b5-89f9-0a56b3e0e93b.jpeg
tags: blogging, programming-blogs, javascript, python, python3, coding, programming-languages, dictionary, coding-challenge, codenewbies, python-beginner, programming-tips, python-projects, python-lists, atm-automated-teller-machine-market-size

---

---

Hey everyone,

So, I wanted to share with you all how I put together this simple ATM system in Python. It's nothing fancy, but it gets the job done!

First off, I set up a couple of dictionaries to keep track of card numbers, PINs, and account balances. It looks something like this:

```python
import time

# Dictionary to store card numbers and corresponding PINs
cardsWithPin = {123456789: 123, 987654321: 345, 234567890: 567, 345678901: 789}

# Dictionary to store card numbers and corresponding account balances
cardsWithAmt = {123456789: 50000, 987654321: 5000, 234567890: 7890, 345678901: 100000}
```

Then, I created functions for different operations like checking balance, withdrawing money, and depositing money. Here's a snippet of that:

```python
# Function to check account balance
def checkBalance(cardNo):
    print(f"Current Balance: Rs.{cardsWithAmt.get(cardNo)}/-")
    time.sleep(0.6)

# Function to withdraw money
def withdraw(cardNo):
    print(f"Initial Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
    try: 
        withdrawAmt=int(input("Enter amount you want to withdraw: "))
        if(cardsWithAmt[cardNo]>=withdrawAmt):
            cardsWithAmt[cardNo]=cardsWithAmt.get(cardNo, 0)-withdrawAmt
            time.sleep(0.6)
            print(f"RS. {withdrawAmt}/- Withdraw Successfully...")
            print(f"Remaining Amount: Rs.{cardsWithAmt[cardNo]}/-")
            time.sleep(0.6)
        else:
            time.sleep(1)
            print("Insufficient Balance...")
            time.sleep(0.6)
    except ValueError:
        print("Please Enter Integer Value...")
    
# Function to deposit money
def deposit(cardNo):
    print(f"Initial Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
    try:
        dipositAmt=int(input("Enter amount you want to deposit:"))
        time.sleep(0.6)
        cardsWithAmt[cardNo] = cardsWithAmt.get(cardNo,0)+ dipositAmt
        print(f"Rs.{dipositAmt}/-are deposited successfully...")
        print(f"Current Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
        time.sleep(0.6)
    except ValueError:
        print("Please Enter Integer Value...")

# Main ATM system function
def atmSystem():
    # Some code here...
```

The `atmSystem` function is where the magic happens. It handles the whole ATM experience, from logging in to performing transactions and quitting the system.

```python
def atmSystem():
    print("======================WELLCOME==========================")
    # Some code here...
```

And that's pretty much it! It's a straightforward program that does what it's supposed to do. Of course, there's always room for improvement, but for now, I'm happy with how it turned out.

Feel free to take a look at the full code and play around with it. If you have any suggestions for improvements or cool features to add, I'm all ears!

Catch you later!

---

And here's the complete code:

```python
import time
cardsWithPin={123456789:123,987654321:345,234567890:567,345678901:789}
cardsWithAmt={123456789:50000,987654321:5000,234567890:7890,345678901:100000}

def checkBalance(cardNo):
    print(f"Current Balance: Rs.{cardsWithAmt.get(cardNo)}/-")
    time.sleep(0.6)

def withdraw(cardNo):
    print(f"Initial Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
    try: 
        withdrawAmt=int(input("Enter amount you want to withdraw: "))
        if(cardsWithAmt[cardNo]>=withdrawAmt):
            cardsWithAmt[cardNo]=cardsWithAmt.get(cardNo, 0)-withdrawAmt
            time.sleep(0.6)
            print(f"RS. {withdrawAmt}/- Withdraw Successfully...")
            print(f"Remaining Amount: Rs.{cardsWithAmt[cardNo]}/-")
            time.sleep(0.6)
        else:
            time.sleep(1)
            print("Insufficient Balance...")
            time.sleep(0.6)
    except ValueError:
        print("Please Enter Integer Value...")

    
    
def deposit(cardNo):
    print(f"Initial Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
    try:
        dipositAmt=int(input("Enter amount you want to deposit:"))
        time.sleep(0.6)
        cardsWithAmt[cardNo] = cardsWithAmt.get(cardNo,0)+ dipositAmt
        print(f"Rs.{dipositAmt}/-are deposited successfully...")
        print(f"Current Balance:Rs.{cardsWithAmt.get(cardNo)}/-")
        time.sleep(0.6)
    except ValueError:
        print("Please Enter Integer Value...")

def atmSystem():
    print("======================WELLCOME==========================")
    try:
        cardNo=int(input("Enter your card number:"))
        if cardNo not in cardsWithPin:
            print("Invalid card no...")
            return
        pin=int(input("Enter pin: "))
        if cardsWithPin.get(cardNo)!=pin:
            print("Invalid pin...")
            return
    except ValueError:
        print("Card Number and Pin should always INTEGER")
        return
    time.sleep(0.5)
    print("Login Successfull...")
    time.sleep(0.4)
    
    while True: 
        print("""Please select any option:
            1).Deposit
            2).Withdraw
            3).Check Balance
            4).Quit
                """)
        operation=int(input("Select option: "))
        match(operation):
            case 1:
                print("You selected Money Deposit...")
                deposit(cardNo)
            case 2:
                print("You selected Withdraw...")
                withdraw(cardNo)
            case 3:
                print("You selected Check Balance...")
                checkBalance(cardNo)
            case 4:
                time.sleep(0.3)
                print("Thank you for using the ATM. Goodbye!")
                return
            case _: 
                print("Invalid option")
                time.sleep(0.6)
    
atmSystem()
```

Feel free to copy and paste it into your Python environment and give it a try! Let me know if you have any questions or suggestions.