# getmempoolentry

`getmempoolentry "txid"`

Returns mempool data for given transaction

## Argument #1 - txid

**Type:** string, required

The transaction id (must be in mempool)

## Result

{                                       (json object)
  "vsize" : n,                          (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
  "weight" : n,                         (numeric) transaction weight as defined in BIP 141.
  "fee" : n,                            (numeric) transaction fee in BTC (DEPRECATED)
  "modifiedfee" : n,                    (numeric) transaction fee with fee deltas used for mining priority (DEPRECATED)
  "time" : xxx,                         (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
  "height" : n,                         (numeric) block height when transaction entered pool
  "descendantcount" : n,                (numeric) number of in-mempool descendant transactions (including this one)
  "descendantsize" : n,                 (numeric) virtual transaction size of in-mempool descendants (including this one)
  "descendantfees" : n,                 (numeric) modified fees (see above) of in-mempool descendants (including this one) (DEPRECATED)
  "ancestorcount" : n,                  (numeric) number of in-mempool ancestor transactions (including this one)
  "ancestorsize" : n,                   (numeric) virtual transaction size of in-mempool ancestors (including this one)
  "ancestorfees" : n,                   (numeric) modified fees (see above) of in-mempool ancestors (including this one) (DEPRECATED)
  "wtxid" : "hex",                      (string) hash of serialized transaction, including witness data
  "fees" : {                            (json object)
    "base" : n,                         (numeric) transaction fee in BTC
    "modified" : n,                     (numeric) transaction fee with fee deltas used for mining priority in BTC
    "ancestor" : n,                     (numeric) modified fees (see above) of in-mempool ancestors (including this one) in BTC
    "descendant" : n                    (numeric) modified fees (see above) of in-mempool descendants (including this one) in BTC
  },
  "depends" : [                         (json array) unconfirmed transactions used as inputs for this transaction
    "hex",                              (string) parent transaction id
    ...
  ],
  "spentby" : [                         (json array) unconfirmed transactions spending outputs from this transaction
    "hex",                              (string) child transaction id
    ...
  ],
  "bip125-replaceable" : true|false,    (boolean) Whether this transaction could be replaced due to BIP125 (replace-by-fee)
  "unbroadcast" : true|false            (boolean) Whether this transaction is currently unbroadcast (initial broadcast not yet acknowledged by any peers)
}

## Examples

bitcoin-cli getmempoolentry "mytxid"

curl --user myusername --data-binary '{"jsonrpc": "1.0", "id": "curltest", "method": "getmempoolentry", "params": ["mytxid"]}' -H 'content-type: text/plain;' http://127.0.0.1:8332/