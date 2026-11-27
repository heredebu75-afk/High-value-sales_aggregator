# ==========================================================
# PROJECT: HIGH VALUE SALES AGGREGATOR
# MODULES: LIST, TUPLE, DICTIONARY
# ==========================================================

# Sales transactions stored in a list of dictionaries
transactions = [
    {"id": 101, "product": "Laptop", "quantity": 2, "price": 55000},
    {"id": 102, "product": "Mouse", "quantity": 5, "price": 500},
    {"id": 103, "product": "Smartphone", "quantity": 3, "price": 25000},
    {"id": 104, "product": "Keyboard", "quantity": 4, "price": 1500},
    {"id": 105, "product": "Monitor", "quantity": 2, "price": 18000},
    {"id": 106, "product": "Tablet", "quantity": 1, "price": 30000},
    {"id": 107, "product": "Headphones", "quantity": 3, "price": 4000},
    {"id": 108, "product": "Gaming PC", "quantity": 1, "price": 85000}
]

# Calculate total value of each transaction
for transaction in transactions:
    transaction["total"] = (
        transaction["quantity"] * transaction["price"]
    )

# Take threshold input from the user
print("=" * 60)
print("          HIGH VALUE SALES AGGREGATOR")
print("=" * 60)

threshold = float(input("Enter minimum sales threshold (Rs.): "))

# Extract high-value transactions using list comprehension
high_value_sales = [
    transaction
    for transaction in transactions
    if transaction["total"] >= threshold
]

# Store premium sales product names in a tuple
premium_products = tuple(
    sale["product"] for sale in high_value_sales
)

# Calculate summary statistics
total_sales = sum(t["total"] for t in transactions)
premium_sales = sum(t["total"] for t in high_value_sales)

number_of_transactions = len(transactions)
premium_count = len(high_value_sales)

average_premium = (
    premium_sales / premium_count
    if premium_count > 0 else 0
)

percentage = (
    (premium_sales / total_sales) * 100
    if total_sales > 0 else 0
)

# Display high-value transactions
print("\n" + "-" * 60)
print("              PREMIUM SALES REPORT")
print("-" * 60)

if high_value_sales:
    print(
        f"{'ID':<8}{'Product':<18}"
        f"{'Qty':<8}{'Total (Rs.)':>15}"
    )
    print("-" * 60)

    for sale in high_value_sales:
        print(
            f"{sale['id']:<8}"
            f"{sale['product']:<18}"
            f"{sale['quantity']:<8}"
            f"{sale['total']:>15,.2f}"
        )
else:
    print("No transactions found above the threshold.")

# Display summary
print("\n" + "=" * 60)
print("                 SALES SUMMARY")
print("=" * 60)

print(f"Total transactions       : {number_of_transactions}")
print(f"Premium transactions     : {premium_count}")
print(f"Total sales              : Rs. {total_sales:,.2f}")
print(f"Premium sales value      : Rs. {premium_sales:,.2f}")
print(f"Average premium sale     : Rs. {average_premium:,.2f}")
print(f"Premium contribution     : {percentage:.2f}%")

# Display tuple
print("\nPremium products tuple:")
print(premium_products)

# Find highest-value transaction
if transactions:
    highest_sale = max(
        transactions, key=lambda t: t["total"]
    )

    print("\nHighest-value transaction:")
    print(f"Product : {highest_sale['product']}")
    print(f"Amount  : Rs. {highest_sale['total']:,.2f}")

# ==========================================================
# VISUAL ANALYSIS
# ==========================================================

print("\n" + "=" * 60)
print("             VISUAL SALES ANALYSIS")
print("=" * 60)

print("\n1. Premium vs Regular Transactions")

regular_count = number_of_transactions - premium_count

print(f"Premium : {'#' * premium_count} ({premium_count})")
print(f"Regular : {'#' * regular_count} ({regular_count})")

print("\n2. Premium Sales Value by Product")

if high_value_sales:
    max_value = max(s["total"] for s in high_value_sales)

    for sale in high_value_sales:
        bar_length = int(
            (sale["total"] / max_value) * 30
        )

        bar = "#" * bar_length

        print(
            f"{sale['product']:<18} "
            f"{bar:<30} "
            f"Rs. {sale['total']:,.0f}"
        )
else:
    print("No premium sales available for analysis.")

print("\n3. Premium Sales Contribution")

print(f"Premium : {'#' * int(percentage / 2)} "
      f"{percentage:.2f}%")

print(f"Regular : {'#' * int((100 - percentage) / 2)} "
      f"{100 - percentage:.2f}%")

print("\n" + "=" * 60)
print("       HIGH VALUE SALES ANALYSIS COMPLETED")
print("=" * 60)