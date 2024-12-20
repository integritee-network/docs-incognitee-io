# Vouchers

Vouchers are a way to share tokens with friends who may not even have a wallet set up yet.

The Incognitee dApp lets you create unique links which you can share as vouchers, either as url or as QR code.

The recipient can open that link and immediately has access to the funds. A voucher is a temporary wallet 
only and everyone who knows the link can spend the funds. Therefore, we suggest to withdraw the funds to a secure wallet swiftly.

# How it works

The app creates a fresh keypair client-side and encodes the private key into the voucher link. The creator of the voucher funds it with a private transfer on Incognitee.

For convenience, all created vouchers are persisted in your browser storage until you deletete them manually. Should the voucher get lost on the way to the recipient, you can recover it.

Notice that the dApp will store and show all vouchers you created on the same machine (with the same browser), irrespective of the account you used to fund it.
