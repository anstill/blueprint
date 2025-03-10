<p align=right><img src="https://i.imgur.com/zNYvmnw.png" width=400 ></p>

# Blueprint

A development environment for TON blockchain for writing, testing, and deploying smart contracts.

### Quick start 🚀

Run the following in terminal to create a new project and follow the on-screen instructions:

```console
npm create ton@latest
```

&nbsp;

### Core features 🔥

* Create a development environment from template in one click - `npm create ton`
* Streamlined workflow for building, testing and deploying smart contracts
* Dead simple deployment to mainnet/testnet using your favorite wallet (eg. Tonkeeper)
* Blazing fast testing of multiple smart contracts in an isolated blockchain running in-process

### Tech stack

1. Compiling FunC with https://github.com/ton-community/func-js (no CLI)
2. Testing smart contracts with https://github.com/ton-community/sandbox
3. Deploying smart contracts with [TON Connect 2](https://github.com/ton-connect), [Tonhub wallet](https://tonhub.com/) or a `ton://` deeplink

### Requirements

* [Node.js](https://nodejs.org) with a recent version like v18, verify version with `node -v`
* IDE with TypeScript and FunC support like [Visual Studio Code](https://code.visualstudio.com/) with the [FunC plugin](https://marketplace.visualstudio.com/items?itemName=tonwhales.func-vscode)

&nbsp;

## Create a new project

1. Run and follow the on-screen instructions: &nbsp;  `npm create ton` &nbsp; or &nbsp; `npx create-ton`
2. (Optional) Then from the project directory: &nbsp; `yarn install` &nbsp; or &nbsp; `npm install`

### Directory structure

* `contracts/` - Source code in [FunC](https://ton.org/docs/develop/func/overview) for all smart contracts and their imports
* `wrappers/` - TypeScript interface classes for all contracts (implementing `Contract` from [ton-core](https://www.npmjs.com/package/ton-core))
  * include message [de]serialization primitives, getter wrappers and compilation functions
  * used by the test suite and client code to interact with the contracts from TypeScript
* `tests/` - TypeScript test suite for all contracts (relying on [Sandbox](https://github.com/ton-community/sandbox) for in-process tests)
* `scripts/` - Deployment scripts to mainnet/testnet and other scripts interacting with live contracts
* `build/` - Compilation artifacts created here after running a build command

### Build one of the contracts

1. You need a compilation script in `wrappers/<CONTRACT>.compile.ts` - [example](https://github.com/ton-community/create-ton/blob/main/template/variants/counter/wrappers/Counter.compile.ts)
2. Interactive: &nbsp; `yarn blueprint build` &nbsp; or &nbsp; `npx blueprint build`
3. Non-interactive: &nbsp; `yarn blueprint build <CONTRACT>`
   * Example: `yarn blueprint build counter`
4. Build results are generated in `build/<CONTRACT>.compiled.json`

### Run the test suite

1. Run in terminal: &nbsp; `yarn test` &nbsp; or &nbsp; `npm test`

### Deploy one of the contracts

1. You need a deploy script in `scripts/deploy<CONTRACT>.ts` - [example](https://github.com/ton-community/create-ton/blob/main/template/variants/counter/scripts/deployCounter.ts)
2. Interactive: &nbsp; `yarn blueprint run` &nbsp; or &nbsp; `npx blueprint run`
3. Non-interactive: &nbsp; `yarn blueprint run <CONTRACT> --<NETWORK> --<DEPLOY_METHOD>`
   * Example: `yarn blueprint run deploycounter --mainnet --tonconnect`

&nbsp;

## Develop a new contract

1. Make sure you have a project to host the contract
2. Interactive: &nbsp; `yarn blueprint create`
3. Non-interactive: &nbsp; `yarn blueprint create <CONTRACT> --type <TYPE>` (type can be `empty` or `counter`)
   * Example: `yarn blueprint create MyNewContract --type empty`

### Contract code

1. Implement the standalone FunC root contract in `contracts/<CONTRACT>.fc`
2. Implement shared FunC imports (if breaking code to multiple files) in `contracts/imports/*.fc`
3. Implement wrapper TypeScript class in `wrappers/<CONTRACT>.ts` to encode messages and decode getters

### Test suite

1. Implement TypeScript tests in `tests/<CONTRACT>.spec.ts`
2. Rely on the wrapper TypeScript class from `wrappers/<CONTRACT>.ts` to interact with the contract

### Compilation and deployment

1. Implement a compilation script in `wrappers/<CONTRACT>.compile.ts`
2. Implement a deployment script in `scripts/deploy<CONTRACT>.ts`
3. Rely on the wrapper TypeScript class from `wrappers/<CONTRACT>.ts` to initialize the contract

&nbsp;

## License

MIT
