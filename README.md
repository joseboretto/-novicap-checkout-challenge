# novicap-checkout-challenge

https://novicap.com/

## Challenge Author 

Nicolas Overloop (Founder of Novicap - CTO)

https://www.linkedin.com/in/nicolas-overloop-ba691b9/

https://github.com/noverloop

https://gist.github.com/noverloop/86c4993b16f589637d06e66a04f4a6c2

## Challenge 

##### Besides providing invoice finance, NoviCap also runs a physical store which sells (only) 3 products:


``` 
Code         | Name                |  Price
-------------------------------------------------
VOUCHER      | NoviCap Voucher      |   5.00€
TSHIRT       | NoviCap T-Shirt      |  20.00€
MUG          | NoviCap Coffee Mug   |   7.50€
```

Various departments have insisted on the following discounts:

 * The marketing department believes in 2-for-1 promotions (buy two of the same product, get one free), and would like for there to be a 2-for-1 special on `VOUCHER` items.

 * The CFO insists that the best way to increase sales is with discounts on bulk purchases (buying x or more of a product, the price of that product is reduced), and demands that if you buy 3 or more `TSHIRT` items, the price per unit should be 19.00€.

NoviCap's checkout process allows for items to be scanned in any order, and should return the total amount to be paid. The interface for the checkout process looks like this (ruby):

```ruby
co = Checkout.new(pricing_rules)
co.scan("VOUCHER")
co.scan("VOUCHER")
co.scan("TSHIRT")
price = co.total
```

Our sales team is constantly adding, removing, and repricing products, so they should be configurable with a json file.

Examples:

    Items: VOUCHER, TSHIRT, MUG
    Total: 32.50€

    Items: VOUCHER, TSHIRT, VOUCHER
    Total: 25.00€

    Items: TSHIRT, TSHIRT, TSHIRT, VOUCHER, TSHIRT
    Total: 81.00€

    Items: VOUCHER, TSHIRT, VOUCHER, VOUCHER, MUG, TSHIRT, TSHIRT
    Total: 74.50€

**The code should:**
- Be written as production-ready code. You will write production code.
- Be easy to grow and easy to add new functionality.
- Have notes attached, explaning the solution and why certain things are included and others are left out.
- Be written in a language you are comforable with as we will do pair programming on your submission in subsequent interviews
- Be as simple as possible. We value clean, minimal, well-designed code; no points for showing off.
---
# Solution 
## Run
```
cat shopping-cart
docker-compose run checkout < shopping-cart
```
## Re Build
```
docker-compose up --build checkout
```

## Development
In order to develop this project you will need:
- JDK 8
- Maven 3

```
mvn package
java -jar ./target/checkout.jar products.json < shopping-cart
```

## code design choices

- **Language**: I chose Java because it is a language that I use in the company I am working on. It is stable and has great performance along with extensive documentation.
- **Build**: Maven.
- **JSON Analyzer**: I choose Jackson based on some articles I read (for example, https://www.baeldung.com/java-json). In short, Jackson has the best performance when working with large files.
- **Tests**: I choose Junit + Mockito because they are well known.
- **Patterns**: I followed the SOLID patterns , program to an interface instead of an implementation, and dependency injection.


