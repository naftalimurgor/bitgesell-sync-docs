# estimatesmartfee

`estimatesmartfee conf_target ( "estimate_mode" )`

Estimates the approximate fee per kilobyte needed for a transaction to begin confirmation within conf\_target blocks if possible and return the number of blocks for which the estimate is valid. Uses virtual transaction size as defined in BIP 141 (witness data is discounted).

## Argument #1 - conf\_target

**Type:** numeric, required

Confirmation target in blocks (1 - 1008)

## Argument #2 - estimate\_mode

**Type:** string, optional, default=CONSERVATIVE

The fee estimate mode.

Whether to return a more conservative estimate which also satisfies a longer history. A conservative estimate potentially returns a higher feerate and is more likely to be sufficient for the desired target, but is not as responsive to short term drops in the prevailing fee market. Must be one of: “UNSET” “ECONOMICAL” “CONSERVATIVE”

## Result

{                   (json object)
  "feerate" : n,    (numeric, optional) estimate fee rate in BTC/kB (only present if no errors were encountered)
  "errors" : [      (json array, optional) Errors encountered during processing (if there are any)
    "str",          (string) error
    ...
  ],
  "blocks" : n      (numeric) block number where estimate was found
                    The request target will be clamped between 2 and the highest target
                    fee estimation is able to return based on how long it has been running.
                    An error is returned if not enough transactions and blocks
                    have been observed to make an estimate for any number of blocks.
}

## Examples

bitcoin-cli estimatesmartfee 6