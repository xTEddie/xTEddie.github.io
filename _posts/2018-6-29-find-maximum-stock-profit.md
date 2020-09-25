---
layout: post
title: Find Maximum Stock Profit
---

### Problem

You have been given a list of stock prices of the day for **Company X**. The index represent the timestamp. The element at index 0 is the initial price of the stock, the element at index 1 is the next recorded price of the stock of that day, etc. 

How can you find the maximum profit possible from the purchase and sale of a single share of **Company X** stock on that day?

For example, if you were given the list of stock prices:

stock_prices = [9, 8, 12, 2, 3, 17]

Then, you would find 15 as the maximum profit (buying at 2 and selling at 17).

### Solution

One thing to think about is that we can't just find the maximum price and lowest price and then substract the two, because the max could come before the min.

A brute force method would be to try every possible combinations, but the time complexity would be **O(n^2)**.

A better solution will be using a **greedy algorithm** approach. We will iterate through the list of stock prices while keeping track of our maximum profit. 

In other words, for every price we will track of the lowest price so far and then check if we can get a better profit than our current max. 

```
def find_max_profit(stocks_prices):

    # Check length
    if len(stocks_prices) < 2:
        raise Exception('Need at least two stock prices!')

    # Default min stock price
    min_stock_price = stocks_prices[0]

    # Default max profit
    max_profit = stocks_prices[1] - stocks_prices[0]

    for price in stocks_prices[1:]:

        # Get min stock price so far
        min_stock_price = min(min_stock_price, price)

        # Check the current price against the min_stock_price for a profit
        comparison_profit = price - min_stock_price

        # Compare against our max_profit so far
        max_profit = max(max_profit, comparison_profit)

    return max_profit
```

We are currently finding the max profit in one pass **O(n)** and in constant space **O(1)**. However, we forgot to address the scenario where the stock price always go down. 

For example, if you were given the list of stock prices:

stock_prices = [100, 80, 60, 40, 20]

The max profit would be 0. It is because the **min_stock_price** gets updated on every iteration and its value is always the same as the **price**.


### Better Solution

In order to fix this, we can calculate the **comparison_profit** first, then compare against the **max_profit**. Calculating the **min_stock_price** will be performed at the end.

```
def find_max_profit2(stocks_prices):

    # Check length
    if len(stocks_prices) < 2:
        raise Exception('Need at least two stock prices!')

    # Default min stock price
    min_stock_price = stocks_prices[0]

    # Default max profit
    max_profit = stocks_prices[1] - stocks_prices[0]

    for price in stocks_prices[1:]:

        # Check the current price against the min_stock_price for a profit
        comparison_profit = price - min_stock_price

        # Compare against our max_profit so far
        max_profit = max(max_profit, comparison_profit)

        # Get min stock price so far
        min_stock_price = min(min_stock_price, price)

    return max_profit
```

Now this piece of code will return a **negative profit** of -20 for the **stock_prices = [100, 80, 60, 40, 20]**.