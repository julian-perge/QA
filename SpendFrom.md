# spendfrom.py utility

Submit completed tests by making a pull request from your fork of this project.

Test environment:

A Linux machine running a raw-transactions-API-capable version of bitcoind/Bitcoin-Qt (version 0.7.2 or git HEAD),
with python and a python jsonrpc library installed.

A testnet wallet that has a greater-than-zero balance and has sent and received bitcoins.

## Bounties:

No bounties for this, I hope people who need the 'coin control' feature will help test.

## Test Setup

1. Backup your main wallet.dat (if it contains any bitcoins; better safe than sorry!)
2. Make sure you have a bitcoin.conf file in your bitcoin [data directory](https://en.bitcoin.it/wiki/Data_directory)
with rpcuser/rpcpassword set.
3. Run bitcoind/Bitcoin-Qt version 0.7.2 or later with the -testnet flag
4. Download https://github.com/gavinandresen/bitcoin-git/raw/spendfrom/contrib/spendfrom/spendfrom.py

If you need testnet bitcoins, ask in the #bitcoin-dev IRC channel or get some from
http://tpfaucet.appspot.com/

## Tests

### List available spending addresses

Run:
```spendfrom.py --testnet```

EXPECT:

See list of addresses and balances.

### Send from one address

Run the following, replacing $ADDRESS and $AMOUNT with an address/amount available to spend:
```spendfrom.py --testnet --from=$ADDRESS --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=$AMOUNT```

EXPECT:
1. transaction id returned
2. transaction sent from your wallet to the testnet faucet (your balance decreases by $AMOUNT)

### Attempt to send too much

Run the following, replacing $ADDRESS with another address that is available to spend and has less than 99 testnet coins::
```spendfrom.py --testnet --from=$ADDRESS --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=99```

EXPECT: error complaining that $ADDRESS doesn't have that many coins.

### Send from one address, change to a second address

Run the following, replacing $ADDRESS1 with another address that has coins, $ADDRESS2 any other address in your wallet,
and $AMOUNT an amount less than the amount available from $ADDRESS1:
```spendfrom.py --testnet --from=$ADDRESS1,$ADDRESS2 --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=$AMOUNT```

EXPECT:
1. transaction id
2. Run bitcoind/bitcoin-qt -testnet getrawtransaction $txid  :  the transaction should have two outputs, one to $ADDRESS2
and the other to the testnet faucet.

### Send from more than one address

Choose two addresses that have coins available (run spendfrom.py --testnet  with no arguments), and total the
amount of coins available from those two addresses. Then run:

```spendfrom.py --testnet --from=$ADDRESS1,$ADDRESS2 --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=$AMOUNT```

EXPECT: transaction id, wallet balance goes down by $AMOUNT

### Send-to-self

Choose an address with coins available, and create a send-to-self transaction for less than the total amount available:

```spendfrom.py --testnet --from=$ADDRESS --to=$ADDRESS --amount=$AMOUNT```

EXPECT: send-to-self transaction created with one output that sends more than $AMOUNT coins from $ADDRESS to $ADDRESS (because
sendfrom.py combines leftover change with $AMOUNT and sends it to $ADDRESS).

### Fee sanity-checks

Attempt to send a tiny amount without paying a fee:

```spendfrom.py --testnet --from=$ADDRESS --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=0.00001```

EXPECT: error

Attempt to send with an outrageous fee:

```spendfrom.py --testnet --from=$ADDRESS --to=mrhz5ZgSF3C1BSdyCKt3gEdhKoRL5BNfJV --amount=0.01 --fee=1.0```

EXPECT: error

### Error: bitcoin not running

1. Quit bitcoind/Bitcoin-Qt
2. Run spendfrom.py

EXPECT: helpful error message
