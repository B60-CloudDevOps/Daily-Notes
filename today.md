How internal domains may look like ?

    roboshop.internal
        mongodb.roboshop.internal
        cart.roboshop.internal
        payment.roboshop.internal

_____________________________________________________________________________________________
    roboshop-prod.internal
        mongodb.roboshop-prod.internal
        cart.roboshop-prod.internal
        payment.roboshop-prod.internal

    roboshop-dev.internal
        mongodb.roboshop-dev.internal
        cart.roboshop-dev.internal
        payment.roboshop-dev.internal

_____________________________________________________________________________________________
    roboshop.internal
        mongodb-dev.roboshop.internal
        cart-dev.roboshop.internal
        payment-dev.roboshop.internal

        mongodb-uat.roboshop.internal
        cart-uat.roboshop.internal
        payment-uat.roboshop.internal

        mongodb-prod.roboshop.internal
        cart-prod.roboshop.internal
        payment-prod.roboshop.internal
__________________________________________________________________________________________________

We can use the same public domain
    > For public DNS Records, we will supply the public ip
    > For private DNS Records, we will supply the private ip

    roboshop.online
        frontend.roboshop.online ---> 100.23.10.26
        catalogue.roboshop.online ---> 10.20.30.10

__________________________________________________________________________________________________

How can I get my public domain ?
    1) We can buy it from the Route53 hosted zones and price is based on the popularity
    2) Or We can buy it from freenom or godaddy or hostiger and can manage it from the Route53


> Tomorrow, please ensure you buy a domain ( .online or .in or .store ) domains are inexpensive
> You can buy it on GoDaddy or Hostinger
> Typically domain activation takes 24hrs of time