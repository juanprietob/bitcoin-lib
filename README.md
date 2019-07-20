# bitcoin-lib

Talk to a bitcoin-core node. 
This library implements all the jsonrpc calls using the [request](https://www.npmjs.com/package/request) library and

## Installation 

----
	npm install bitcoin-lib
----

### Usage example

----
	const BitcoinLib = require("bitcoin-lib");
	var bitlib = new BitcoinLib();

	bitlib.start()
    .then(function(){
        return bitlib.getrawtransaction([transactionid, true]);
    })
    .then(function(res){
    	var tx = tes.result;
    	console.log(tx);
	})
	.then(function(){
    	return bitlib.getbalance('wallet name', ["*", 6]);
	})
    .catch(function(err){
    	console.error(err);//Something went wrong during initialization/authentication to the bitcoin-core node	
	})
----

### Calls for wallets

Unfortunatelly, the RPC endpoint for wallets is different. In my opinion, this should be changed in
bitcoin-core. Instead of a path, it should be a query parameter or just an additional parameter. 
The RPC endpoint for wallets is 'http://127.0.0.1:8332/wallet/<walletname>'. In the example above, the 
wallet name is the first parameter and the parameters for the call are in the array. 


#### bitcoin-core documentation

Check the official documentation of the API for [bitcoin-core](https://bitcoin.org/en/developer-reference#bitcoin-core-apis)

This is just a print of 'bitcoin-cli help' for reference. All of this functions are available in this library. 

----
	== Blockchain ==
	getbestblockhash
	getblock "blockhash" ( verbosity )
	getblockchaininfo
	getblockcount
	getblockhash height
	getblockheader "blockhash" ( verbose )
	getblockstats hash_or_height ( stats )
	getchaintips
	getchaintxstats ( nblocks "blockhash" )
	getdifficulty
	getmempoolancestors "txid" ( verbose )
	getmempooldescendants "txid" ( verbose )
	getmempoolentry "txid"
	getmempoolinfo
	getrawmempool ( verbose )
	gettxout "txid" n ( include_mempool )
	gettxoutproof ["txid",...] ( "blockhash" )
	gettxoutsetinfo
	preciousblock "blockhash"
	pruneblockchain height
	savemempool
	scantxoutset "action" [scanobjects,...]
	verifychain ( checklevel nblocks )
	verifytxoutproof "proof"

	== Control ==
	getmemoryinfo ( "mode" )
	getrpcinfo
	help ( "command" )
	logging ( ["include_category",...] ["exclude_category",...] )
	stop
	uptime

	== Generating ==
	generate nblocks ( maxtries )
	generatetoaddress nblocks "address" ( maxtries )

	== Mining ==
	getblocktemplate "template_request"
	getmininginfo
	getnetworkhashps ( nblocks height )
	prioritisetransaction "txid" ( dummy ) fee_delta
	submitblock "hexdata" ( "dummy" )
	submitheader "hexdata"

	== Network ==
	addnode "node" "command"
	clearbanned
	disconnectnode ( "address" nodeid )
	getaddednodeinfo ( "node" )
	getconnectioncount
	getnettotals
	getnetworkinfo
	getnodeaddresses ( count )
	getpeerinfo
	listbanned
	ping
	setban "subnet" "command" ( bantime absolute )
	setnetworkactive state

	== Rawtransactions ==
	analyzepsbt "psbt"
	combinepsbt ["psbt",...]
	combinerawtransaction ["hexstring",...]
	converttopsbt "hexstring" ( permitsigdata iswitness )
	createpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )
	createrawtransaction [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )
	decodepsbt "psbt"
	decoderawtransaction "hexstring" ( iswitness )
	decodescript "hexstring"
	finalizepsbt "psbt" ( extract )
	fundrawtransaction "hexstring" ( options iswitness )
	getrawtransaction "txid" ( verbose "blockhash" )
	joinpsbts ["psbt",...]
	sendrawtransaction "hexstring" ( allowhighfees )
	signrawtransactionwithkey "hexstring" ["privatekey",...] ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
	testmempoolaccept ["rawtx",...] ( allowhighfees )
	utxoupdatepsbt "psbt"

	== Util ==
	createmultisig nrequired ["key",...] ( "address_type" )
	deriveaddresses "descriptor" ( range )
	estimatesmartfee conf_target ( "estimate_mode" )
	getdescriptorinfo "descriptor"
	signmessagewithprivkey "privkey" "message"
	validateaddress "address"
	verifymessage "address" "signature" "message"

	== Wallet ==
	abandontransaction "txid"
	abortrescan
	addmultisigaddress nrequired ["key",...] ( "label" "address_type" )
	backupwallet "destination"
	bumpfee "txid" ( options )
	createwallet "wallet_name" ( disable_private_keys blank )
	dumpprivkey "address"
	dumpwallet "filename"
	encryptwallet "passphrase"
	getaddressesbylabel "label"
	getaddressinfo "address"
	getbalance ( "dummy" minconf include_watchonly )
	getnewaddress ( "label" "address_type" )
	getrawchangeaddress ( "address_type" )
	getreceivedbyaddress "address" ( minconf )
	getreceivedbylabel "label" ( minconf )
	gettransaction "txid" ( include_watchonly )
	getunconfirmedbalance
	getwalletinfo
	importaddress "address" ( "label" rescan p2sh )
	importmulti "requests" ( "options" )
	importprivkey "privkey" ( "label" rescan )
	importprunedfunds "rawtransaction" "txoutproof"
	importpubkey "pubkey" ( "label" rescan )
	importwallet "filename"
	keypoolrefill ( newsize )
	listaddressgroupings
	listlabels ( "purpose" )
	listlockunspent
	listreceivedbyaddress ( minconf include_empty include_watchonly "address_filter" )
	listreceivedbylabel ( minconf include_empty include_watchonly )
	listsinceblock ( "blockhash" target_confirmations include_watchonly include_removed )
	listtransactions ( "label" count skip include_watchonly )
	listunspent ( minconf maxconf ["address",...] include_unsafe query_options )
	listwalletdir
	listwallets
	loadwallet "filename"
	lockunspent unlock ( [{"txid":"hex","vout":n},...] )
	removeprunedfunds "txid"
	rescanblockchain ( start_height stop_height )
	sendmany "" {"address":amount} ( minconf "comment" ["address",...] replaceable conf_target "estimate_mode" )
	sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount replaceable conf_target "estimate_mode" )
	sethdseed ( newkeypool "seed" )
	setlabel "address" "label"
	settxfee amount
	signmessage "address" "message"
	signrawtransactionwithwallet "hexstring" ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
	unloadwallet ( "wallet_name" )
	walletcreatefundedpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime options bip32derivs )
	walletlock
	walletpassphrase "passphrase" timeout
	walletpassphrasechange "oldpassphrase" "newpassphrase"
	walletprocesspsbt "psbt" ( sign "sighashtype" bip32derivs )

	== Zmq ==
	getzmqnotifications
----


## Testing 

### Run all tests

----
	npm test
----

