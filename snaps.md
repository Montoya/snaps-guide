<Section name="1. Introduction" description="Introduction to MetaMask Snaps">

## Extend the functionality of MetaMask

[Snaps](https://metamask.io/snaps/) is a system that allows anyone to safely extend the capabilities of MetaMask. A snap is a program that runs in an isolated environment that can customize the wallet experience.

For example, a snap can add new APIs to MetaMask, add support for different blockchain protocols, or modify existing functionality using internal APIs. Snaps is a new way to create web3 end user experiences, by modifying MetaMask in ways that were impossible before.

## Secure execution

Snaps execute in a sandboxed environment based on [Hardened JavaScript](https://docs.agoric.com/guides/js-programming/hardened-js.html) by Agoric. Snaps uses a permissions model for protecting user data and respecting user consent. 

## Developer preview software

Snaps is pre-release software. To try Snaps, install [MetaMask Flask](https://metamask.io/flask/), a canary distribution for developers that provides access to upcoming features.

## Question

<Quiz id={"89b8i"} /> ~ put quiz here!

</Section>


<Section name="2. Overview of Features" description="Features">

## Features

At present, snaps can (1) create new RPC methods for websites to call, (2) call many of the same RPC methods that websites can call, and (3) access a limited set of snap-exclusive RPC methods. The following metrhods are currently live in MetaMask Flask. 

## Question

<Quiz id={"bv6ew"} />

<Quiz id={"qrakr"} />

</Section>


<Section name="3. Registering an ENS" description="Getting your ">

## How to register

Registering your first ENS name is super easy through the use of the [ENS Manager](http://app.ens.domains/).

![Search your Name](https://i.imgur.com/D4ntUeO.png)

Once you arrive at the name's page and the name is available. (Checkout the **register** tab). You should see a live calculation of the costs for registering that name. Names with fewer then 5 characters, and recently expired names have different costs. For more information on registration costs, check our [FAQ](https://docs.ens.domains/permanent-registrar-faq#how-much-will-the-yearly-renewals-cost).

![](https://i.imgur.com/xlcWoJ4.png)

Once you click the **Request to Register** button and confirm the transaction the manager will reserve the name for you. After this you will need to wait for one minute. This is done to protect you from frontrunning and ensures you get the name you desired.

![](https://i.imgur.com/D8EUxod.png)

![](https://i.imgur.com/pGMw8Ce.png)

![](https://i.imgur.com/pbTJ2vq.png)

Great! Our name is now reserved for our second transaction. You can now click the **Register** button to complete the registration process.

![](https://i.imgur.com/3NrIBEl.png)

**Congratulations!** 🎉 You now own an ENS name! To set it as your **Primary Name** click the **"Set As Primary ENS Name"** button and follow the steps.

## How to set Avatar

To set your avatar you can go to the [ENS Manager](https://app.ens.domains/) and select the name you would like to set an **Avatar** for.

Now you are on the page simply hit **ADD/EDIT RECORD** and scroll down to the **avatar** field.

![](https://i.imgur.com/fLFw8Ey.png)

### The Avatar Field

The Avatar Field can be filled with a variety of different types of text. In the example below I am uploading an **IPFS** link (using **ipfs://**), however you could also use **Arweave**, a link to an NFT (using [CAIP-29](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-29.md)), base64 image, or any regular **HTTP(S)** url will do.

![](https://i.imgur.com/Scbp1AW.png)

### Question

<Quiz id={"r3wki"} />


<Quiz id={"2mtcw"} />


</Section>

<Section name="4. Integrate ENS" description="Integrate ENS into your Project">

## Resolving ENS names for Users

With the help of your favourite library such as [Ethers](https://docs.ethers.io/v5/api/providers/provider/#Provider--ens-methods), [Wagmi](https://wagmi.sh/docs/hooks/useEnsName), [ENS.js](https://www.npmjs.com/package/@ensdomains/ensjs), [Web3.js](https://web3js.readthedocs.io/en/v1.2.0/web3-eth-ens.html), [Web3j](https://github.com/web3j/web3j), [KEthereum](https://github.com/komputing/KEthereum/tree/master/ens), [web3.py](https://web3py.readthedocs.io/en/stable/ens_overview.html), [go-ens](https://github.com/wealdtech/go-ens), and many more.

![User Profile & Lookup example](https://i.imgur.com/9G8yvJ2.png)

It's that easy! Now your dApp is ready to show everyone's names everywhere! And don't forget to fallback to addresses when the user doesn't have a name.

#### React Example

Below is an example snippet of what this would look like using [wagmi](https://wagmi.sh/docs/hooks/useEnsName).

```tsx
import { useAccount, useEnsAvatar, useEnsName } from 'wagmi';
const shortenAddress = (address) => `${address.substr(0, 5)}...${address.substr(-4)}`;
export const UserProfile = () => {
    const { address } = useAccount();
    const { data: name, isSuccess: isNameSuccess } = useEnsName({ address });
    const { data: avatar, isSuccess: isAvatarSuccess } = useEnsAvatar({
        addressOrName: address,
    });
    return (
        <div>
            <div>
                {isAvatarSuccess && avatar ? (
                    <img src={avatar} />
                ) : (
                    <img src="" />
                )}
            </div>
            <div>
                {isNameSuccess && name ? (
                    <div>
                        <span>{name}</span>
                        <span>{shortenAddress(address)}</span>
                    </div>
                ) : (
                    <div>{address}</div>
                )}
            </div>
        </div>
    );
};
```

## Retrieving Address from Name

You may however want users to be able to search for each other, mention one another, or even challenge each other to a game of tic tac to. Now should this be the case there is the **resolveName** functionality that allows you to enter any valid ENS name and get back the address.

![Address Resolution & Lookup Example](https://i.imgur.com/yaMUwih.png)

## Question

<Quiz id={"qppyi"} />


</Section>

<Section name="Dev Resources" description="Developer Resources">

## ENS Developer Resources

### [Quickstart](https://docs.ens.domains/dapp-developer-guide/ens-enabling-your-dapp)

Everything you need to know to get started implementing ENS in your dApp.

### [Docs](https://docs.ens.domains)

Your go-to location for protocol information and examples.

### [Metadata Service](https://metadata.ens.domains/docs)

Metadata service that allows for fetching data .

### [Libraries](https://docs.ens.domains/dapp-developer-guide/ens-libraries)
- [Ethers](https://docs.ethers.io/v5/api/providers/provider/#Provider--ens-methods)
- [Wagmi](https://wagmi.sh/docs/hooks/useEnsName)
- [ENS.js](https://www.npmjs.com/package/@ensdomains/ensjs)
- [Web3.js](https://web3js.readthedocs.io/en/v1.2.0/web3-eth-ens.html)
- [Web3j](https://github.com/web3j/web3j)
- [KEthereum](https://github.com/komputing/KEthereum/tree/master/ens)
- [web3.py](https://web3py.readthedocs.io/en/stable/ens_overview.html)
- [go-ens](https://github.com/wealdtech/go-ens)

### [Mirror](https://ens.mirror.xyz/)

For the latest news and updates about the ENS Ecosystem.

### [Medium](https://medium.com/the-ethereum-name-service)

For our archive of Articles.

![More Coming Soon](https://i.imgur.com/TaB3p5o.png)

</Section>
