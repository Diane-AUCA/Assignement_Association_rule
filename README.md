Groceries Association Rule Analysis

This project uses association rule mining on almost 10,000 grocery transactions. The Apriori algorithm was used to find products that customers often buy together and to measure how strong these relationships are.

This analysis was done as part of the Unsupervised Learning Method course assignment on association rule learning.

About this assignment

When people go shopping, the products they buy are usually not completely random. For example, someone who buys bread may also buy butter, while someone who buys beef may also buy vegetables.

This project looks at these buying patterns using the Groceries dataset, which contains 9,835 transactions and 169 different products.

The main goal is not only to find the most popular products, but also to find out which products are actually related to each other. For example, whole milk is the most frequently purchased product, but being popular does not necessarily mean that it has a strong relationship with other products. Some of the more interesting relationships can be found among products that are not the most popular.

The data, briefly

Each row in groceries.csv represents one shopping trip and contains the products bought during that trip. There is no customer ID or timestamp, so the analysis only looks at the products in each basket.

A typical basket contains around 4–5 items. There are 169 different products in total, but each transaction contains only a small number of them. This makes the dataset quite sparse.

Because of this, it would be difficult to manually check all possible product combinations. The Apriori algorithm helps find the combinations that appear often enough to be useful.

How the analysis works

The notebook (Groceries_Association_Rules.ipynb) follows five main steps:

Load and explore the data – Read the transaction file, count the products, and find the 10 most purchased items.
Encode the data – Convert the transactions into a one-hot encoded basket matrix, with one column for each product.
Find frequent itemsets – Apply the Apriori algorithm with a minimum support of 1%. This means that an item combination must appear in at least about 99 of the 9,835 transactions to be considered frequent.
Generate association rules – Create rules in the form X → Y using a minimum confidence of 30%. The rules are then evaluated using support, confidence, and lift.
Interpret the results – Identify the important rules and explain what they could mean in a real grocery store.
The three main measures

Support shows how often a combination of products appears in all transactions.

Confidence shows how often Y is bought when a customer has already bought X.

Lift shows how much more likely Y is to be bought with X compared with what we would expect by chance. A lift above 1 shows a positive association, while a value close to 1 means there is little or no strong relationship.

What the numbers show

The analysis found 213 frequent product pairs and 32 frequent triples using the 1% support threshold. From these itemsets, 125 association rules met the 30% confidence requirement.

Some results are worth looking at more closely.

The "everyone buys this" pattern.
{other vegetables, whole milk} has the highest support among the product pairs, appearing in 7.48% of all transactions. The rule {other vegetables} → {whole milk} also has high support, but its lift is only 1.51.

This means that the combination is very common, but the relationship between the two products is not extremely strong. This is partly because both products are already popular on their own.

The more interesting pattern.
{citrus fruit, other vegetables} → {root vegetables} has the highest lift in the dataset, with a value of 3.295. This means that customers who buy citrus fruit and other vegetables are more than three times as likely to also buy root vegetables compared with what would be expected by chance.

However, this combination is not very common. Its support is only 1.04%. So, although it is a strong relationship, it happens in a relatively small number of transactions.

The highest confidence pattern.
{citrus fruit, root vegetables} → {other vegetables} has the highest confidence, at 58.6%. This means that when customers buy citrus fruit and root vegetables together, other vegetables are also included in the basket about 58.6% of the time.

These examples show that support, confidence, and lift measure different things. A rule can have high support without having a very strong relationship, while another rule can have high lift but appear in fewer transactions.

Figures

## Figures

![Top 10 Most Frequently Purchased Items](figure1_top10_items.png)

![Distribution of Basket Sizes](figure2_basket_size_distribution.png)

![Top 10 Frequent Itemsets by Support](figure3_top10_itemsets.png)

![Association Rules: Support vs Confidence](figure4_rules_scatter.png)

![Distribution of Lift Across All Rules](figure5_lift_distribution.png)

## Turning this into store decisions

A few ways a supermarket could actually act on these results:

 **Shelf placement:** move root vegetables closer to the meat aisle  the beef → root vegetables rule carries a lift of ~3.0, suggesting genuine intent, not coincidence.
 **A bundled offer:** package citrus fruit, other vegetables, and root vegetables together as a "stew starter" promotion, riding on that highlift relationship.
 **Checkout recommendations:** something like "you bought butter  add whole milk?" is a natural fit given its 49.7% confidence and solid lift (1.95).

## Things to keep in mind

This kind of analysis has real boundaries:

 No customer IDs, so there's no way to tell if the same shopper is behind repeat patterns.
 No timestamps, so seasonal effects (holiday baking, summer grilling, etc.) are invisible here.
 No pricing or margin data, so a rule being statistically strong doesn't mean it's the most *profitable* one to act on.
 Correlation, not causation  a rule showing beef and root vegetables together doesn't mean buying beef makes someone buy root vegetables; it just means the two tend to cooccur.
 Everything here is sensitive to the thresholds chosen (1% support, 30% confidence)  different cutoffs would surface a different set of rules.

## Getting started

```bash
pip install pandas numpy matplotlib mlxtend jupyter
jupyter notebook
```

Then open `Groceries_Association_Rules.ipynb` (keep it in the same folder as `groceries.csv`) and run all cells top to bottom.

## Files in this project

 `groceries.csv`  the raw transaction data
 `Groceries_Association_Rules.ipynb`  full analysis, code, and figures
 `Groceries_Report`  written report with answers to each assignment question
 `README.md`  this file

## Sources

 Agrawal, R., & Srikant, R. (1994). *Fast Algorithms for Mining Association Rules.* Proceedings of the 20th VLDB Conference.
 Raschka, S. (2018). *MLxtend: Providing machine learning and data science utilities and extensions to Python's scientific computing stack.* Journal of Open Source Software, 3(24), 638.
