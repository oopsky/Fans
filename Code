const Web3 = require('web3');

// 连接到FTM网络
const web3 = new Web3('https://');

// 您的账户地址和私钥
const senderAddress = '0x';

const privateKey = '0x';  // 私钥

// 接收方地址
const recipientAddress = '0x';

async function sendTransaction() {
  while (true) {
    // 构建交易对象
    const transaction = {
      to: recipientAddress,
      value: web3.utils.toWei('0', 'ether'),
      gasLimit: web3.utils.toHex(21960),
      // 2890这个值可根据网络的实时gas-200来更改，这样基本上是最低的gas
      gasPrice: web3.utils.toHex(web3.utils.toWei('2890', 'gwei')),
      data: '0x646174613a2c7b2270223a226672632d3230222c226f70223a226d696e74222c227469636b223a2266616e73222c22616d74223a223130303030227d'
    };

    const nonce = await web3.eth.getTransactionCount(senderAddress);
    transaction.nonce = nonce;

    try {
      const signedTx = await web3.eth.accounts.signTransaction(transaction, privateKey);

      const receipt = await web3.eth.sendSignedTransaction(signedTx.rawTransaction);
      console.log(receipt.transactionHash);
    } catch (error) {
      console.error(error);
    }

    await new Promise(resolve => setTimeout(resolve, 10));
  }
}

sendTransaction();
