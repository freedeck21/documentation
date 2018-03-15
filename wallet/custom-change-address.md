# Creating a Custom Change Address

You may have noticed that when you send Zoin to another wallet, the transaction details and blockchain explorer return change to your wallet using a different address. The reason for this is the input and output approach to transactions in a blockchain. When you send a transaction, it references the block in which you received those funds. For example, let's say you have two transactions. A deposit to your wallet of 10 Zoin and a withdraw of 2 Zoin. When you send the 2 Zoin, the deposit \(input\) of 10 Zoin will be used, giving 8 Zoin back in change. If you do not specify the change address, a random address is generated in the wallet.

As of Zoin wallet version 0.13.2, you can configure what address you would like change to go to. For example, perhaps you want to use a single address in your wallet and you want all change to be deposited back to that single address. This guide will demonstrate how to do so.

## Procedure

1. In your wallet, drop down the **Zoin Core **menu in the top-left and select **Settings **on Windows or **Preferences **on OSX.

   ![](/assets/zoin-menu.png)

1. Next, select the **Wallet **tab and check the **Enable coin control features **checkbox and click **OK**.

   ![](/assets/wallet-options.png)

1. Go to the **Send **tab and click the **Transaction **icon as shown below.

   ![](/assets/wallet-transaction-menu.png)

1. The following dialog box will pop up.

   ![](/assets/transaction-menu-dialog.png)

2. Select the **Custom change address **checkbox, paste the address from your wallet that you want to use, and click **OK**. Now, whenever you receive change from a transaction it will be deposited to this address.



