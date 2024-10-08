This interface is used to transfer files to another territory.

```golang
// TerritoryFileDelivery transfer files to another territory
//   - user: file owner account
//   - fid: file id
//   - target_territory: transfer to the target territory
//
// Return:
//   - string: block hash
//   - error: error message
func (c *ChainClient) TerritoryFileDelivery(user []byte, fid string, target_territory string) (string, error)
```

Example code:
```golang
package main

import (
    "context"
    "fmt"
    "time"

    sdkgo "github.com/CESSProject/cess-go-sdk"
)

// Substrate well-known mnemonic:
//
//   - https://github.com/substrate-developer-hub/substrate-developer-hub.github.io/issues/613
//   - cXgaee2N8E77JJv9gdsGAckv1Qsf3hqWYf7NL4q6ZuQzuAUtB
var MY_MNEMONIC = "bottom drive obey lake curtain smoke basket hold race lonely fit walk"

var RPC_ADDRS = []string{
    //testnet
    "wss://testnet-rpc.cess.network/ws/",
}

func main() {
    sdk, err := sdkgo.New(
        context.Background(),
        sdkgo.ConnectRpcAddrs(RPC_ADDRS),
        sdkgo.Mnemonic(MY_MNEMONIC),
        sdkgo.TransactionTimeout(time.Second*10),
    )
    if err != nil {
        panic(err)
    }
    defer sdk.Close()

    fmt.Println(sdk.TerritoryFileDelivery(sdk.GetSignatureAccPulickey(),"fid", "target_territory"))
}
```