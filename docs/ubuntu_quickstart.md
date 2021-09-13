## Steps to Run Linux Build

1. Download Ubuntu Desktop 20.04 LTS ISO from the [Ubuntu website](https://ubuntu.com/download/desktop)

2. Create a VM with the image from step 1 (process depends on your machine - not covered here)

(These first two steps do not apply if you have a native Linux machine or are using WSL command line)

3. Download/copy .sh file from [this link](https://gist.githubusercontent.com/obskein/8efb025cc41e598a4eaa8b9e6ef9aa82/raw/3ccdcf63e873613c998a002f32f34604d8765aea/install_xgt.sh)

4. `chmod +x install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located

5. `./install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located
	- this will take 10-15 minutes

6. `sudo apt install ruby-full`

7. `sudo gem install xgt-ruby`

8. `cd xgt`

9. `rake configure`

10. `rake make`
	- this will take 10-15 minutes

13. `cd ..`

14. `nano runXGT.sh`

15. Copy and paste the following format into the new file, replacing the empty values with your wallet and private recovery key:

```
#/bin/sh

export wallet_name=your-wallet-address
export recovery_private=your-private-recovery-key
export witness_private=your-private-recovery-key

cd xgt &&
  MINING_DISABLED=FALSE \
  MINING_THREADS=4 \
  XGT_INSTANCE_INDEX=1 \
  XGT_WALLET=$wallet_name \
  XGT_WIF=$recovery_private \
  XGT_RECOVERY_PRIVATE_KEY=$recovery_private \
  XGT_WITNESS_PRIVATE_KEY=$witness_private \
  rake run
```

Set `MINING_DISABLED=TRUE` if you are setting up a sync/seed node. The value of `MINING_THREADS` depends on your machine. Run `ctrl-o` to save and `ctrl-x` to exit.

16. `chmod +x runXGT.sh`

17. `./runXGT.sh`
