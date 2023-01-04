# Gitcoin OpenData Hackathon using Ocean Protocol

Ocean Protocol allows for decentralized sharing of data and algorithms. Contestants are strongly incentivised to use Ocean's technology stack to decentralize access control to algorithms and/or deploy ERC725Y as soulbound tokens for preventing misuse of DAO proposal mechanisms.

## 0. Key Details

- Challenge: Creating insightful anti-Sybil algorithms and packaging them into composable legos, using decentrealised technologies. 
- Kickoff: Jan 5th, 2023
- Submission deadline: Tuesday Jan 31st, 2023 at 23:59 UTC
- Total Prize pool: $40,000 in bounties

**Outline of this README**

This readme describes 2 different ways that participants can use to get free bonus points during the hackathon:

1. Publish your algorithms as ERC721 using the [Ocean Market](https://market.oceanprotocol.com/publish/1) frontend
2. Use Ocean [Data NFTs](https://docs.oceanprotocol.com/core-concepts/datanft-and-datatoken#what-is-a-data-nft) as [ERC725Y](https://github.com/ERC725Alliance/erc725/blob/main/docs/ERC-725.md) via [Ocean.py](https://github.com/oceanprotocol/ocean.py) or [Ocean.js](https://github.com/oceanprotocol/ocean.js)

**NOTE:** Before submitting, make sure you copy your [DID](https://docs.oceanprotocol.com/core-concepts/did-ddo#did) and attach it to your submission.


## 1. Use Ocean Market frontend

Ocean Market provides a convenient interface to publish data assets. Data assets can be datasets, algorithms, images, location information, audio, video, sales data, or combinations of all!

To publish on the Ocean Marketplace, you must first get MATIC or ETH to pay for gas fees, and host your assets on a decentralized storage like Arweave or IPFS.

To host your data assets on Arweave you have two options:

1. In a webapp, using [ardrive.io](https://www.ardrive.io). [Ocean Docs](https://docs.oceanprotocol.com/using-ocean-market/asset-hosting#arweave) has more info.
2. In code, using [pybundlr library](https://github.com/oceanprotocol/pybundlr).

Once the above is completed, take the transaction ID from your hosting service and head over to [Ocean Market](https://market.oceanprotocol.com/publish/1) to get started with publishing. Follow the steps and if you need more information feel free to ask for support in our dedicated [Discord channel](https://discord.gg/JK4rq7KBGh) or visit our [docs](https://docs.oceanprotocol.com/using-ocean-market/marketplace-publish-data-asset).


## 2. Use Ocean Data NFTs as ERC725Y

The ERC725y feature enables the NFT owner to input and update information in a key-value store. These values can be viewed externally by anyone and are highly useful building blocks for various Sybil protection approaches. As an example, DAOs can use Ocean data NFTs to provide great amount of resistance in preventing misuse of DAO proposal mechanisms. 

Ocean data NFTs can also be used to [Login with Web3](https://github.com/oceanprotocol/ocean.py/blob/main/READMEs/profile-nfts-flow.md) and allow a dApp to not only connect to the user's wallet, but also access profile data that the user has privately shared to it. In fact, Ocean data NFTs can essentially be used as [Soulbound Tokens](https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID4105763_code1186331.pdf?abstractid=4105763&mirid=1) as well. 


### 2.1 Via Ocean.py

Before getting started, ensure that you've already [installed Ocean.py](https://github.com/oceanprotocol/ocean.py/blob/main/READMEs/install.md) and [set it up remotely](https://github.com/oceanprotocol/ocean.py/blob/main/READMEs/setup-remote.md)


#### 2.1.1 Publish data NFT

In Python console:
```python
from ocean_lib.models.arguments import DataNFTArguments
data_nft = ocean.data_nft_factory.create(DataNFTArguments('NFT1', 'NFT1'), alice)
```

#### 2.1.2 Add key-value pair to data NFT

```python
# Key-value pair
key = "fav_color"
value = b"blue"
# prep key for setter
from web3.main import Web3
key_hash = Web3.keccak(text=key)  # Contract/ERC725 requires keccak256 hash
# set
data_nft.setNewData(key_hash, value, {"from": alice})
```

#### 2.1.3 Retrieve value from data NFT

```python
value2_hex = data_nft.getData(key_hash)
value2 = value2_hex.decode('ascii')
print(f"Found that {key} = {value2}")
```

That's it! All data was stored and retrieved from on-chain without using Ocean Provider or Ocean Aquarius (though the latter can help for fast querying & retrieval).

This way, we can also encrypt the data. Under the hood, it uses [ERC725](https://erc725alliance.org/), which augments ERC721 with a well-defined way to set and get key-value pairs.

If you need more information about Ocean ERC725y feel free to ask for support in our dedicated [Discord channel](https://discord.gg/JK4rq7KBGh). Alternatively, you can visit the full [README](https://github.com/oceanprotocol/ocean.py/blob/main/READMEs/key-value-flow.md) or our [docs](https://docs.oceanprotocol.com/core-concepts/datanft-and-datatoken#implementation-in-ocean-protocol).


### 2.2 Via Ocean.Js

Before getting started, ensure that you've already [installed Ocean.js](https://github.com/oceanprotocol/ocean.js#-installation--usage).

Using Ocean Data NFTs as [ERC725Y](https://github.com/ERC725Alliance/erc725/blob/main/docs/ERC-725.md) via Ocean.js can be helpful for dApp developers, particularly if you have prior experience with javascript.

The process involves creating a Data NFT (which represents the base-IP on-chain) and a datatoken (which will be used to purchase the dataset). Access the full [README](https://github.com/oceanprotocol/ocean.js/blob/main/CodeExamples.md#8-using-erc725-key-value-store) to get started.

If you need more information about Ocean ERC725y feel free to ask for support in our dedicated [Discord channel](https://discord.gg/JK4rq7KBGh) or visit our [docs](https://docs.oceanprotocol.com/core-concepts/datanft-and-datatoken#implementation-in-ocean-protocol).
