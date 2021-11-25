# Fi-Link
FiLink A data provider transfers deals info to chainlink Oracle

## Problem
As a user on other blockchain, we do not have a native way to know if a storage deal is active on Filecoin network.
## Solutions 
By build a filecoin data adapter to chainlink oracle. It can give other blockchain the capability of validation if a data is onchain

The adapter is scaning the data from Flecoin blockchain and post the deal info to polygon network, the deal info is by the following format:


```json
{

    "DealId": 58160,
    "dealCid": "bafyreifo2pp5d4se44xu32p5ikm3qjzmfv7ihbmdsilz7j5wii7h7ne3gm",
    "messageCid": "bafy2bzacebyuyuxr23e2n3njhtltcuc7sc73cuumzd2fww4mt4ivtzg2zn6um",
    "height": 455035,
    "pieceCid": "baga6ea4seaql3pcfitmlane3nbrlcitb4ffzdkkswy4e2tn4tf67muicdcueiki",
    "verifiedDeal": false,
    "storagePricePerEpoch": "976562 AttoFIL",
    "signature": "rWJeBFkmGZTAnIitvM6NiRpn8vqwlRAjr4PpMHmfL6Kb86qeXU99DtHWmjW8WyARAFn3mTUtB4+rlibfEUFlts4cAESxfHPiuOciVj0r0d8Y3te0axEZETGsJeLQPPkY",
    "signatureType": "bls",
    "createdAt": "2021-11-24 07:57:30",
    "pieceSizeFormat": "2.00 MiB",
    "satrtHeight": 466508,
    "endHeight": 1980929,
    "client": "t3u7pumush376xbytsgs5wabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbhwpnojqd3jie6ermpwvvq",
    "clientCollateralFormat": "0 AttoFIL",
    "provider": "t024557",
    "providerTag": "",
    "providerIsVerified": 0,
    "providerCollateralFormat": "0 AttoFIL",
    "status": 0

}

```
### Chainlink Adapter - DATA DAO 

Data Dao signs the node for providing data feeds to the web3 blockchains like polygoin, bsc, eth.
Every data deal has a deal ID, it is an unique id on filecoin network used for tracking deal info.
Filecoin data adatper provides deal ids for other blockchain system to check if the deal exists on filecoin network.

## Sample Use Case
### Polygon Chain Payment for Filecoin storage

Data source -Filecoin -> data aggregator-Filswan -> data provider- Filswan -> Chainlink Adapter - DATA DAO -> MCP DAO unlock fund based on Chainlink Adapter

### Deal Matching
scheduler to update status to trigger DAO signature for unlock event
* get deal_id by proposal_cid
* get deal_id from Chainlink filecoin adapter
    * if matches trigger DAO signature
        * match client_address
        * match deal_cid (proposal_cid)
    * else waiting for next check cycle


