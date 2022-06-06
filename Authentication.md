Authentication

New User
Fund User

New User 
Navigate to Memo external auth with necessary parameters
URL

https://memo.cash/account/link?
Parameters

return_url=http://localhost:8080/auth-complete&
address=12kap...
Click Connect on Memo
Transaction to fund address is created and broadcast
Redirect auth complete
URL

http://memo.cash/auth-complete?
Parameters

api_token=c97b1a33...
api_temp_key=dab9b452...
parent_address=12kap...
Get key
jmemo.Client.Api.Key.Get(api_token, api_temp_key, function (response) {
    var api_secret = response.secret;
});
Create link request using API (linking)
jmemo.Client.Link.CreateRequest(api_token, api_secret, address, parent_address, "", function (unsignedTx) {
    var key = jmemo.Wallet.GetHDChild(mnemonic, jmemo.Wallet.Path.MainAddressPath());
    var signedTx = jmemo.Wallet.Sign.SignTx(unsignedTx.raw, key);
    jmemo.Client.Tx.BroadcastAndWait(signedTx.toHex(), function (response) {
        var requestTxHash = jmemo.Wallet.Util.GetTxRawHash(signedTx.toHex());
    });
});
Complete linking
jmemo.Client.Link.FinishAccept(api_token, api_temp_key, requestTxHash, function (signedTx) {
    jmemo.Client.Tx.BroadcastAndWait(signedTx.raw);
});

Fund User 
Navigate to Memo [link](https://memocash.github.io/#api-linking) with necessary parameters
URL
https://memo.cash/acount/link?=https://memo.cash/profile/1GtdcmSM3RBe71JJoAAc5Y8o48vmQgt2Ve
Parameters

return=http://memo.cash/request-payment-complete&
address=12kap...&
amount=10000
Click [Connect]() on Memo
Redirect request payment complete
URL

https://memo.cash/profile/1GtdcmSM3RBe71JJoAAc5Y8o48vmQgt2Ve/request-payme
