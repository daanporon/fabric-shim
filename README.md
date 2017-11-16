[![NPM](https://nodei.co/npm/fabric-shim.svg?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/fabric-shim/)

[![Version](https://badge.fury.io/js/fabric-shim.svg)](http://badge.fury.io/js/fabric-shim) [![Build Status](https://jenkins.hyperledger.org/buildStatus/icon?job=fabric-chaincode-node-merge-x86_64)](https://jenkins.hyperledger.org/view/fabric-chaincode-node/job/fabric-chaincode-node-merge-x86_64)

`fabric-shim` provides the APIs for application developers to implement "Smart Contracts" for the Hyperledger Fabric backend, also known as "Chaincodes". Detailed explanation on the concept and programming model can be found here: [http://hyperledger-fabric.readthedocs.io/en/latest/chaincode.html](http://hyperledger-fabric.readthedocs.io/en/latest/chaincode.html).

## Installation
```sh
npm install fabric-shim
```

## Usage
The [chaincode interface](https://fabric-shim.github.io/ChaincodeInterface.html) contains two methods to be implemented:
```javascript
const shim = require('fabric-shim');

const Chaincode = class {
	async Init(stub) {
		// use the instantiate input arguments to decide initial chaincode state values

		// save the initial states
		await stub.putState(key, Buffer.from(aStringValue));

		return shim.success(Buffer.from('Initialized Successfully!'));
	}

	async Invoke(stub) {
		// use the invoke input arguments to decide intended changes

		// retrieve existing chaincode states
		let oldValue = await stub.getState(key);

		// calculate new state values and saves them
		let newValue = oldValue + delta;
		await stub.putState(key, Buffer.from(newValue));

		return shim.success(Buffer.from(newValue.toString()));
	}
};
```

Start the chaincode process and listen for incoming endorsement requests:
```javascript
shim.start(new Chaincode());
```

## API Reference
Visit [fabric-shim.github.io](https://fabric-shim.github.io/) and click on "Classes" link in the navigation bar on the top to view the list of class APIs.

## Support
Tested with node.js 8.9.0 (LTS).

## License

This package is distributed under the
[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0),
see LICENSE.txt for more information.