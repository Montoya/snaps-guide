<Section name="1. Introduction" description="Introduction to MetaMask Snaps">

## Extend the functionality of MetaMask

[Snaps](https://metamask.io/snaps/) is a system that allows anyone to safely extend the capabilities of MetaMask. A snap is a program that runs in an isolated environment that can customize the wallet experience.

For example, a snap can add new APIs to MetaMask, add support for different blockchain protocols, or modify existing functionality using internal APIs. Snaps is a new way to create web3 end user experiences, by modifying MetaMask in ways that were impossible before.

## Secure execution

Snaps execute in a sandboxed environment based on [Hardened JavaScript](https://docs.agoric.com/guides/js-programming/hardened-js.html) by Agoric. Snaps uses a permissions model for protecting user data and respecting user consent. 

## Developer preview software

Snaps is pre-release software. To try Snaps, install [MetaMask Flask](https://metamask.io/flask/), a canary distribution for developers that provides access to upcoming features.

_Note: You cannot run MetaMask Flask alongside MetaMask. It is recommended to install it in a separate browser profile, and you should not use any of your existing accounts in Flask._

## Question

<Quiz id={"89b8i"} /> ~ put quiz here!

</Section>


<Section name="2. Overview of Features" description="Features">

## Features

At present, snaps can (1) create new RPC methods for websites to call, (2) call many of the same RPC methods that websites can call, and (3) access a limited set of snap-exclusive RPC methods. The following methods are currently live in MetaMask Flask: 

#### Display a custom confirmation screen in MetaMask &bull; [Learn more](./snaps-rpc-api.html#snap-confirm)

Show a MetaMask popup with custom text and buttons to approve or reject an action. This can be used to create requests, confirmations, and opt-in flows for a snap.

#### Notify users in MetaMask &bull; [Learn more](./snaps-rpc-api.html#snap-notify)

MetaMask Flask introduces a generic notifications interface that can be utilized by any snap with the notifications permission. A short notification text can be triggered by a snap for actionable or time-sensitive information.

#### Store and manage data on your device &bull; [Learn more](./snaps-rpc-api.html#snap-managestate)

Store, update, and retrieve data securely, with encryption by default.

#### Control non-EVM accounts and assets in MetaMask &bull; [Learn more](./snaps-rpc-api.html#snap-getbip44entropy)

Derive BIP-32 and BIP-44 keypairs based on the Secret Recovery Phrase without exposing it. With the power to manage keys, you can build snaps to support a variety of blockchain protocols.

#### Populate MetaMask's pre-transaction window with custom transaction insights

Bring your insights, anti-phishing, and security solutions to the MetaMask UI with the transaction insights API.

## Question

<Quiz id={"bv6ew"} />

<Quiz id={"qrakr"} />

</Section>


<Section name="3. Getting Started" description="Learn how to build your own snap">

## Pre-requisites

First, make sure you have an up to date Chromium or Firefox browser and make sure you have [MetaMask Flask](https://metamask.io/flask/) installed in a separate browser profile from any other installation of MetaMask. Then, make sure you have [Node.js](https://nodejs.org/) version 16.0 (it is recommended to use [nvm](https://github.com/nvm-sh/nvm)). 

## Quick start using our template

Start building your own snap using [our template](https://github.com/MetaMask/template-snap-monorepo) built with TypeScript and React. Clone the repository [via GitHub](https://github.com/MetaMask/template-snap-monorepo/generate) and open it on your local machine using e.g. the command line.

> NB: Snaps should work with the LTS version of Node.js, but we recommend using the version specified in the template's `.nvmrc` file. If you use [nvm](https://github.com/nvm-sh/nvm) you can switch easily with calling `nvm use` at the root of the project.

From the root of the repo, install the dependencies:

```shell
yarn
```

Start the development server:

```shell
yarn start
```

You should now be serving both (1) the front-end and (2) the snap locally. Time to check it out in action with MetaMask Flask at [`http://localhost:3000/`](http://localhost:3000/). 

1. Click the Connect button and the MetaMask Flask extension should pop up and require you to approve the template snap's permissions. 
2. Once connected, try out the Send message button to display a custom message within a confirmation screen in MetaMask.

You've now successfully connected, installed, and interacted with your snap.


### Question

<Quiz id={"r3wki"} />


<Quiz id={"2mtcw"} />


</Section>

<Section name="4. Building your snap" description="Learn how to build your own snap with this example">

## Learn how to build your own snap by modifying the template

Customize your snap by editing and expanding `index.ts` in the `packages/snap/src` folder.

Initially it contains an example request that utilizes the `snap_confirm` method to display a custom confirmation screen:

```ts
import { OnRpcRequestHandler } from '@metamask/snap-types';
import { getMessage } from './message';

export const onRpcRequest: OnRpcRequestHandler = ({ origin, request }) => {
  switch (request.method) {
    case 'hello':
      return wallet.request({
        method: 'snap_confirm',
        params: [
          {
            prompt: getMessage(origin),
            description:
              'This custom confirmation is just for display purposes.',
            textAreaContent:
              'Edit the source code to make your snap do what you want.',
          },
        ],
      });
    default:
      throw new Error('Method not found.');
  }
};
```

Modify the text in the `description` or `textAreaContent` field. Refresh the dapp in your browser, and click the **Connect** button to reinstall the snap.

The next time you click the **Send message** button, you will see the updated text in the confirmation screen.

Congratulations! You just learned how to build your own snap!

## Question

<Quiz id={"qppyi"} />


</Section>

<Section name="Dev Resources" description="Developer Resources">

## More Resources

### [MetaMask Snaps Deveopment Guide](https://docs.metamask.io/guide/snaps-development-guide.html)

Covers a wide range of topics related to developing snaps.

### Open-Source Example Snaps
- FilSnap for Filecoin: [Repo](https://github.com/chainsafe/filsnap) &bull; [Demo](https://filsnap.chainsafe.io/)
- StarkNet Snap: [Repo](https://github.com/ConsenSys/starknet-snap) &bull; [Demo](https://app.starknet-snap.consensys-solutions.net/)
- Password Manager Snap: [Repo](https://github.com/ritave/snap-passwordManager)

### Talks and Workshops
- [How to Revolutionize Web3 Development in 20 Minutes - ETH Denver, Feb 2022](https://www.youtube.com/watch?v=KhpCS8EbKTE)
- [Introduction to MetaMask Snaps - ETH Rio, March 2022](https://www.youtube.com/watch?v=XL3OduRT8js)
- [Workshop: Expand MetaMask with Snaps - EthCC Paris, Aug 2022](https://www.youtube.com/watch?v=BWII6nkT-2w)

### Stay in touch

Have questions? Need help? Head to the [MetaMask Snaps Discussion Board](https://github.com/MetaMask/snaps-skunkworks/discussions) on GitHub to talk to the platform team. 

</Section>