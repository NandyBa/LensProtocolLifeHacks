# LensProtocolLifeHacks

This repo is here to save life hacks regarding [Lens Protocol](https://lens.xyz)

## Get list of followers for a specific user
*We will asume you know the user address and you want to track his default Lens profile*
1. [Get user's Lens profile id](#get-default-lens-profile-id-of-a-specific-address)
2. [Get user's Follow contract](#get-users-follow-contract)
3. [Get user's total number of followers](#get-users-total-number-of-followers)
4. [Get all user's followers](#get-all-users-followers)

## Check if one user follow another:
*Example: Check if Alice follow Bob*

1. [Get Bob Lens Profile Id](#get-default-lens-profile-id-of-a-specific-address)
2. [Get Bob's Follow contract](#get-users-follow-contract)
3. Call [Bob's FollowNFT](#get-users-follow-contract) as FollowNFT proxy ([doc](https://docs.lens.xyz/docs/deployed-contract-addresses)) **balanceOf** function.

balanceOf(AliceAddress)

**return** balance
- if balance >= 1 Alice follow Bob
- if balance == 0 Alice don't follow Bob

## Get user profile picture:
*Call [LensHub Proxy](#smart-contracts) **getProfile** function*

getProfile(LensProfileId)

**return**
We are interested in the 5th element the **imageURI** (type string)

**List of the complet data structure return**
- pubCount	uint256	The publication count associated with this profile
- followModule	address	The follow module associated with this profile, if any
- followNFT	address	The follow NFT associated with this profile, if any
- handle	string	The handle associated with this profile
- **imageURI**	string	The URI associated with this profile's image *(What we interrested in)*
- followNFTURI	string	The URI associated with this profile's follow NFT

### Smart contracts:
#### Polygon Mainnet Addresses :
- LensHub Proxy: 0xDb46d1Dc155634FbC732f92E853b10B288AD5a1d ([doc](https://docs.lens.xyz/docs/deployed-contract-addresses))

#### Mumbai Testnet Addresses (Polygon Testnet) :
- LensHub Proxy: 0x60Ae865ee4C725cd04353b5AAb364553f56ceF82 ([doc](https://docs.lens.xyz/docs/deployed-contract-addresses))


## Get default Lens profile id of a specific address:

*Call [LensHub Proxy](#smart-contracts) **DefaultProfile** function*

DefaultProdile(walletAddress)

**return** LensProfileId

## Get user's follow contract:

*Call [LensHub Proxy](#smart-contracts) **getFollowNFT** function*

getFollowNFT(LensProfileId)

**return** FollorNFTAddress

## Get user's total number of followers
*Call [FollowNFT](#get-users-follow-contract) as FollowNFT proxy ([doc](https://docs.lens.xyz/docs/deployed-contract-addresses)) **totalSupply** function*

totalSupply()

**return** totalSupply (type unit256)

## Get all user's followers
*Loop Call [FollowNFT](#get-users-follow-contract) as FollowNFT proxy ([doc](https://docs.lens.xyz/docs/deployed-contract-addresses)) **tokenId** function until tokenId > totalSupply*

ownerOf(tokenId)

**return** followerAddress
