# faucet
Faucet cloudflare worker for prefunding bounty hunters' addresses

## How it works
1. Some 3rd party service (for example [ubiquity bot](https://github.com/ubiquity/ubiquibot)) sends a `POST` request with the `address` query param, for example: `https://ubq-faucet.workers.dev/?address=0x01`
2. [Openzeppelin Defender Relay](https://docs.openzeppelin.com/defender/v2/manage/relayers) service prefunds the `0x01` address with some gas payment tokens (`XDAI`, `ETH`, etc...) if the following conditions are met:
    - wallet address exists in the ubiquity bot's DB (i.e. the wallet is registered by some bounty hunter)
    - this is the 1st issue solved by a bounty hunter (i.e. the registered wallet address hasn't got any permits)
    - wallet address has 0 gas tokens amount

## How to run locally
1. Setup env variables in the `.dev.vars` file:
```
# Environment variables used for development build on `yarn start`

# openzeppelin defender relay API key
RELAY_KEY=
# openzeppeling defender relay secret
RELAY_SECRET=

# supabase DB URL
SUPABASE_URL=
# supabase DB secret key
SUPABASE_KEY=

# fund amount in wei
CLAIM_FEE=
```
2. Run `yarn start` to start a local cloudflare worker instance
