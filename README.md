# For the class Software Development Fundamentals

As per the title, this project is done by a group of student from Cakrawala University with members consisting of:
1. Daniel Satria (Lead developer)
2. Muhammad Hasbi Nurkhalis
3. Fajar
4. Roby Cahya Insani
for the class 'Software Development Fundamentals 05' (SDF05), which is taught professor Prabowo Yoga.

## The assignment

For the first assignment we had been told to refactor a code, with the semantic being:
```
A function that returns calculation results from an order form = (individualPrice * quantity) * (10% if > 100, other than that 5*) + shippingFee (if a member then it is free, if not fee of shipping must be paid)
```
which we had to apply said logic unto a pre-existing code that is as follows:

```
def f(a, b, c, d, e):
    x = a * b
    S = 0
    for i in c:
        S = S + i
    if s > 100:
        x = x * 0.9
    else:
        x = x * 0.95
    t = 0
    for i in c:
        t = t + i
    if d:
        X = X + 0
    else:
        X = X + e
    return x
```

Of which can also be seen and ran in its authenticity withing the file name theoriginal.ipynb; whereby many developers can spot all that is wrong with said code with relative ease. Besides the application of the logic from the semantic previously mentioned, the refactorization itself will include renaming all vague variables to its proper designated title/purpose. That being said tehe first thing that needed to be done was with renaming of the variables "a, b, c, d, e" and its function:

```
def orderTotal(individualPrice, quantity, isMember, shippingFees)
```

some key eyed readers might have realized that one alphabet will be missing here, that is becaause taking into consideration the semantic; for the sake of efficiency, there is no need for a 5th variable to be used in the function's parameters. Negation of redunancy should also be the goal of a program lauding itself as clean. As for the next part of the cleansing process, there is a matter of the variables "x, s, t", in which it would be best if those vague alphabets were to be turned into "subtotal, discountedTotal, shippingCost" respectively. To elucidate as to why those were the names picked, we shall put it in simple bulleted point explanation:
1. f -> orderTotal, this is because the function's purpose is to calculate what the total would be.
2. a -> individualPrice, is meant to showcase that it stores the price of one item.
3. b -> quantity, show the amount of items that has been ordered.
4. c -> 404, technically was the variable that is booted out, the reasoning is because the original 'for i in c' loops did not actually contribute to the stated order calculations.
5. d -> isMember, pretty self explnatory which is good.
6. e -> shippingFee, the delivery charge.
7. x -> subTotal, this is the result from the multiplication of individualPrice and quantity.
8. s -> discountedTotal, the variable that shows the result of the final price if discount was applicable.
9. t -> shippingCost, after checking if isMember is true or not, this will be the variable that says if the shippingFee becomes nullified.

Now that the renaming process has been completed, next is the complete refactorization code:

```
def orderTotal(individualPrice, quantity, isMember, shippingFee):
    subTotal = individualPrice * quantity

    if subTotal > 100:
        discountedTotal = subTotal * 0.90
    else:
        discountedTotal = subTotal * 0.95

    if isMember:
        shippingCost = 0
    else:
        shippingCost = shippingFee

    return discountedTotal + shippingCost
```