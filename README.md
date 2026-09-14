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
A function that returns calculation results from an order form = (individualPrice * quantity) * (10% if total-item > 100, other than that 5*) + shippingFee (if a member then it is free, if not fee of shipping must be paid)
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

    if quantity > 100:
        discountedTotal = subTotal * 0.90
    else:
        discountedTotal = subTotal * 0.95

    if isMember:
        shippingCost = 0
    else:
        shippingCost = shippingFee

    return discountedTotal + shippingCost
```

## The Reflection

Then comes reflection, in which we can commence from the part of renaming the entire program itself, each decision though have been properly given an explanation from an objective stand point, as per the more subjective parts such as using the came case technique, where the beginning letter of a word is made small and if there is a second word that starting letter will then be capitalized, come from personal preferences; the assumptions and hope for it to still be readable for the collective programs that might come after us. While the core concept of the program itself did not change, the parts that did however, such as removing the for loop and focusing on the if else was a heavy decision to make, however one we think is for the best since said loop was doing nothing for the program itself, had it still been added then it would have been calculating 'discountedTotal = discountedTotal + i' while it is in the range of c, where c itself does not have a clear range and logic of what it is; then there is a matter of testing, you couldn't test the original code at all, there was only errors so we were visibly confused on how to do so without first changing the program, even then the program itself, since you cannot run the code is some 's' & 'x' variables were uppercase; however irregardless it was tested to the best of our ability, where:
1. 'a'/individualPrice = 1000
2. 'b'/Quantity = 101
3. 'c' = 5 (no clear direction)
4. 'd'/isMember = no
5. 'e'/shippingFee= 5000
and the results were different but expected to be so, because the one prior to refactorization uses the sum of 'c' to determine the discount instead of the order's quantity, which lead the program NOT giving the discount despite the quantity being eligible, which then caused the result for pre-refactorization to be higher (100950) to post (95900); to drive the point home, the original had used the 'c' input to give out a discount, however 'c' itself does not have a clear direction of what it is. Hypothetically we make c the quantity instead of b, but then what would b be? Remeber that the semantic dictates that the TOTAL-ITEM be the one that determines the discount, and that could come from c and c alone but b would still need to be something; logically if b were to be anything else that would mean subTotal would come from individualPrice * b, and if it isn't quantity it does not fufill the semantic of "(harga_satuan × jumlah)" or in english "(individualPrice * quantity)". admittedly there is vagueness if what 'total-item' is, is it its own variable? If so what difference does it hold from quantity/jumlah? Does it mean the total price  of all the items combined? But that's the point of subtotal calculating the multiplication result of individualPrice * quantity, it becomes the total of all items combined. total-item becomes a bit too enigmatic in this sense, which is why it was difficult determaining whether or not it is quantity. Prior to this we also tested out subtotal in place of 'c', which also abide by the ligoc HOWEVER, in the context of INDONESIAN RUPIAH, this would mean that someone would need to buy items worth only beneath a hundred perak; subTotal can only work if the context is for US DOLLARS, since it is possible for them to spend beneath 100 dollars and not get the discount.

So because of that, that was the number one dilemma of the entire project, determining what 'c' is, which was not as straightforward as just saying it is the variable totalItem, because as per mentioned it ends up making the questions of "what is totalItem?" "Is it not quantity?" "Is it not subTotal". However we still decide to include one version where 'c' was made into the variable totalItem.