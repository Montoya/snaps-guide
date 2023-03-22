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

What can you do with Snaps? 

A. Add new APIs to MetaMask

B. Add support for different blockchain protocols

C. Modify existing functionality using internal MetaMask APIs

**D. All of the above**

How does Snaps allow devs to extend MetaMask while protecting user data? 

A. By using a centralized registry for approved snaps

B. By using new encryption methods

**C. By using a sandboxed environment with a permissions model**

D. By using confirmation screens frequently

</Section>


<Section name="2. Overview of Features" description="Features">

At present, snaps can (1) create new RPC methods for websites to call, (2) call many of the same RPC methods that websites can call, and (3) access a limited set of snap-exclusive RPC methods. The following methods are currently live in MetaMask Flask: 

#### Display custom dialogs in MetaMask 

Show a MetaMask popup with custom content. These dialogs can be alerts, confirmation flows, or even prompts for input from the user. [Learn more](https://docs.metamask.io/guide/snaps-rpc-api.html#snap-dialog)

#### Notify users in MetaMask 

MetaMask Snaps introduces a generic notifications interface that can be utilized by any snap with the notifications permission. A short notification text can be triggered by a snap for actionable or time-sensitive information. [Learn more](https://docs.metamask.io/guide/snaps-rpc-api.html#snap-notify)

#### Store and manage data on your device 

Store, update, and retrieve data securely, with encryption by default. [Learn more](https://docs.metamask.io/guide/snaps-rpc-api.html#snap-managestate)

#### Control non-EVM accounts and assets in MetaMask 

Derive BIP-32 and BIP-44 keypairs based on the Secret Recovery Phrase without exposing it. With the power to manage keys, you can build snaps to support a variety of blockchain protocols. [Learn more](https://docs.metamask.io/guide/snaps-rpc-api.html#snap-getbip32entropy)

#### Populate MetaMask's pre-transaction window with custom transaction insights

Bring your insights, anti-phishing, and security solutions to the MetaMask UI with the transaction insights API. [Learn more](https://docs.metamask.io/guide/snaps-exports.html#ontransaction)

## Question

Which of these is not a Snaps Platform method currently available in MetaMask Flask?

**A. Deploy an ERC721 contract**

B. Notify users in MetaMask

C. Show custom transaction insights

D. Store and manage data on your device

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
2. Once connected, try out the Send message button to display a custom message within a dialog in MetaMask.

You've now successfully connected, installed, and interacted with your snap.


### Question

Which of these is not a pre-requisite for developing your own snap? 

A. MetaMask Flask

B. Node.js version 16

**C. Stable Diffusion**

D. Latest Chromium or Firefox browser


</Section>

<Section name="4. Building your snap" description="Learn how to build your own snap with this example">

## Learn how to build your own snap by modifying the template

Customize your snap by editing and expanding `index.ts` in the `packages/snap/src` folder.

Initially it contains an example request that utilizes the `snap_dialog` method to display a custom confirmation screen:

```ts
import { OnRpcRequestHandler } from '@metamask/snaps-types';
import { panel, text } from '@metamask/snaps-ui';

export const onRpcRequest: OnRpcRequestHandler = ({ origin, request }) => {
  switch (request.method) {
    case 'hello':
      return snap.request({
        method: 'snap_dialog',
        params: {
          type: 'Confirmation',
          content: panel([
            text(`Hello, **${origin}**!`),
            text('This custom confirmation is just for display purposes.'),
            text(
              'But you can edit the snap source code to make it do something, if you want to!',
            ),
          ]),
        },
      });
    default:
      throw new Error('Method not found.');
  }
};
```

> The "hello" method is exported by the snap, meaning that it can be called by a dapp after connecting to the snap. This is how a snap can have its own API for dapps: by exporting methods to be called by dapps. Any dapp can connect to this snap and call the "hello" method to display this custom dialog. 

Modify the content of any `text(...)` container. Refresh the dapp in your browser, and click the **Connect** button to reinstall the snap.

The next time you click the **Send message** button, you will see the updated text in the dialog.

Congratulations! You just learned how to build your own snap!

## Question

Which method is called by the dapp in the template example to display the custom dialog? 

A. confirm

**B. hello**

C. invoke

D. render


</Section>

<Section name="Dev Resources" description="Developer Resources">

## More Resources

You can find templates, tutorials, and example projects in the [MetaMask Snaps Getting Started Guide](https://github.com/MetaMask/snaps-monorepo/discussions/675).

### Stay in touch

Have questions? Need help? Head to the [MetaMask Snaps Discussion Board](https://github.com/MetaMask/snaps-skunkworks/discussions) on GitHub to talk to the platform team. 

</Section>