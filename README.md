<div align="center">
  <h1 align="center">Carbon Protocol on Starknet</h1>
  <h3 align="center">Carbonable contracts written in Cairo for StarkNet.</h3>
</div>

## Usage

> ## ⚠️ WARNING! ⚠️
>
> This repo contains highly experimental code.
> Expect rapid iteration.
> **Use at your own risk.**

### Set up the project

### 🎉 Install

```bash
protostar install
```

### ⛏️ Compile

```bash
protostar build
```

### 🌡️ Test

```bash
# Run all tests
protostar test

# Run only unit tests
protostar test tests/units

# Run only integration tests
protostar test tests/integrations
```

### 🌐 Test account

If you want a fresh account for tests, you can deploy an account with the following command:

```bash
starknet deploy_account --network=<network>
```

It will generate the account information into the `~/.starknet_accounts/starknet_open_zeppelin_accounts.json` file.  
See also starknet [documentation](https://www.cairo-lang.org/docs/hello_starknet/account_setup.html#creating-an-account) for more details.

### 💋 Format code

```bash
cairo-format -i src/**/*.cairo tests/**/**/*.cairo
```

### 📝 Documentation

#### Generation

```bash
cd docs
kaaper generate ../src ./data
python build.py
callgraphs.sh
```

## 🚀 Deployment

### Inputs

To manage inputs sent to constructor during the deployment, you can customize the [config files](./scripts/configs/).

### Prepare the contracts before tests

After deployment, the **admin** account (according to parameters) is the owner of all contracts.
So far, you have to do the following actions manually:

- Change the NFT contract owner from **admin** to **Minter contract**
  - How: _Voyager > Write contract > `transferOwnership`_
  - Verify: _Voyager > Read contract > `owner`_
- Approve the **Minter contract** to spend the **admin payment tokens**
  - How: Voyager > _Write contract > `approve`_
  - Verify: Voyager > _Read contract > `allowance`_
- Buy NFT through the **Minter contract**
  - How: _Voyager > Write contract > `buy`_
  - Verify: _Voyager > Read contract > `balanceOf` (of the NFT contract)_
