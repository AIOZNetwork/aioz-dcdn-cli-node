## AIOZ dCDN CLI Node

Official dCDN CLI Node implementation of the AIOZ Network.

## What is AIOZ dCDN CLI Node?

AIOZ dCDN CLI Node is the software to become an AIOZ Node in AIOZ dCDN. AIOZ Node contributes storage capacity, network bandwidth and computing power to the AIOZ dCDN and gets rewards in AIOZ Tokens.

## Requirements

* Windows 10 version 22H2 64-bit or above
* Ubuntu 14.06 64-bit or above
* macOS Catalina version 10.15 or above

## Getting started

### Windows
Download and extract the latest AIOZ dCDN CLI Node. The scripts below are written for Windows PowerShell.
```shell
curl.exe -LO https://github.com/AIOZNetwork/aioz-dcnd-cli-node/files/13559439/aioznode-windows-amd64-1.1.0.zip
Expand-Archive -Path aioznode-windows-amd64-1.1.0.zip -DestinationPath .
ren aioznode-windows-amd64-1.1.0.exe aioznode.exe
```

Verify the node is runnable
```shell
.\aioznode.exe version
```
The output should be the version of AIOZ dCDN Node.

Generate new mnemonic phrase and private key
```shell
.\aioznode.exe keytool new --save-priv-key privkey.json
```
`--save-priv-key` write the private key to file

Response
```json
{
        "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
        "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
        "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFInQXiZtHevsw7gFKvbZXCqFunK3pMjV0I\"}",
        "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SDtubqMUGKn+7doBCCOfegAI9OGMIbE=\"}",
        "mnemonic": "rain wing olive skate effort present long myself combine giant vote stay sweet bundle agree lock connect glide absent spider effort attitude enemy mouse"
}
```
**IMPORTANT NOTE**: Make sure to backup and secure your mnemonic phrase as it will be used in case of migration or recovering your node.

Run the node
```shell
.\aioznode.exe start --home nodedata --priv-key-file privkey.json
```
`--home` data folder of the node

`--priv-key-file` the private key file which the node starts with. If you do not specify the private key file, the node will ask for it from the standard input stream.

Note: 
Because AIOZ dCDN CLI Node automatically updates itself by downloading and replacing the executable file, make sure to set file permission to writable.
AIOZ dCDN CLI Node has to stop to perform auto update, it should be run as Windows Service to start again after update and at system boot.

### macOS and Linux

Download the latest AIOZ dCDN CLI Node

For macOS
```shell
curl -LO https://github.com/AIOZNetwork/aioz-dcnd-cli-node/files/13559428/aioznode-darwin-amd64-1.1.0.tar.gz
tar xzf aioznode-darwin-amd64-1.1.0.tar.gz
mv aioznode-darwin-amd64-1.1.0 aioznode
```

For Linux
```shell
curl -LO https://github.com/AIOZNetwork/aioz-dcnd-cli-node/files/13559433/aioznode-linux-amd64-1.1.0.tar.gz
tar xzf aioznode-linux-amd64-1.1.0.tar.gz
mv aioznode-linux-amd64-1.1.0 aioznode
```

Verify the node is runnable
```shell
./aioznode version
```
The output should be the version of AIOZ dCDN Node.

Generate new mnemonic phrase and private key
```shell
./aioznode keytool new --save-priv-key privkey.json
```
`--save-priv-key` write the private key to file

Response
```json
{
        "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
        "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
        "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFInQXiZtHevsw7gFKvbZXCqFunK3pMjV0I\"}",
        "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SDtubqMUGKn+7doBCCOfegAI9OGMIbE=\"}",
        "mnemonic": "rain wing olive skate effort present long myself combine giant vote stay sweet bundle agree lock connect glide absent spider effort attitude enemy mouse"
}
```
**IMPORTANT NOTE**: Make sure to backup and secure your mnemonic phrase as it will be used in case of migration or recovering your node.

Run the node
```shell
./aioznode start --home nodedata --priv-key-file privkey.json
```
`--home` data folder of the node

`--priv-key-file` the private key file which the node starts with. If you do not specify the private key file, the node will ask for it from the standard input stream.

**Note**: 
Because AIOZ dCDN CLI Node automatically updates itself by downloading and replacing the executable file, make sure to set file permission to writable.
AIOZ dCDN CLI Node has to stop to perform auto update, it should be run with `launchctl`(macOS) or `systemctl`(Linux) to start it again after update and at system boot.

## Usage

### View node status
```shell
./aioznode.exe stats
```
Note: This command requires a running node, if your node is not on default port `1317`, you need to specify it with the flag `--endpoint`

Response
```json
{
        "storage": {
                "total_count": 4864,
                "total_size": 149967615893
        },
        "delivery": {
                "upstream_speed": 0
        }
}
```

### View reward
```shell
./aioznode.exe reward balance
```
Note: This command requires a running node, if your node is not on default port `1317`, you need to specify it with the flag `--endpoint`

Response
```json
{
        "balance": [
                {
                        "denom": "attoaioz",
                        "amount": "7218886258271998637"
                }
        ],
        "storage_earned": [
                {
                        "denom": "attoaioz",
                        "amount": "810423534750216148"
                }
        ],
        "delivery_earned": [
                {
                        "denom": "attoaioz",
                        "amount": "7525653191257749557"
                }
        ],
        "withdraw": [
                {
                        "denom": "attoaioz",
                        "amount": "1100000000000000000"
                }
        ],
        "delivery_counter": 16521
}
```

### Withdraw reward
```shell
./aioznode.exe reward withdraw --address 0x9A20600a143745404f1AA1C69Bd280f4bD5B4408 --amount 1aioz --priv-key-file privkey.json
```
This command requires a running node. If your node is not on default port `1317`, you need to specify it with the flag `--endpoint`. 

`--address` the address to withdraw the reward to. The rewards is transferred in **AIOZ Chain**.

`--amount` the amount of reward to withdraw. The unit can be `aioz` or `attoaioz`. 1 aioz equal 10^18 attoaioz. Minimum withdraw is 1 aioz. Example values: `1aioz`, `1.1aioz`, `1100000000000000000attoaioz`.

`--priv-key-file` the private key file which the node started with. If you do not specify the private key file, the node will ask for it from the standard input stream.

Response
```json
{
        "txid": "2604F553B62B70136967811B14BA8DB5706A2FA86EF7FD1A6899ECB3EF944D59"
}
```

### Recover private key from mnemonic phrase
```shell
.\aioznode.exe keytool recover "rain wing olive skate effort present long myself combine giant vote stay sweet bundle agree lock connect glide absent spider effort attitude enemy mouse" --save-pri-key privkey.json
```
`--save-pri-key` write the private key to file.

Response
```json
{
        "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
        "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
        "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFInQXiZtHevsw7gFKvbZXCqFunK3pMjV0I\"}",
        "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SDtubqMUGKn+7doBCCOfegAI9OGMIbE=\"}"
}
```
