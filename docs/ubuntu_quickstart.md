## Steps to Run Linux Build

1. Download Ubuntu Desktop 20.04 LTS ISO from the [Ubuntu website](https://ubuntu.com/download/desktop)

2. Create a VM with the image from step 1 (process depends on your machine - not covered here)

(These first two steps do not apply if you have a native Linux machine or are using WSL command line)

3. Download/copy .sh file from [this link](https://gist.githubusercontent.com/obskein/fbfd8d87660297e8be7edf01921ab7a8/raw/4a1b03b31814fd96890cfb7401bbf60a8c657a90/install_xgt.sh)

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

export seed_host=98.33.76.100:2001,xgt.rag.pub:2001,xgt2.rag.pub:2001,45.138.27.42:2001,68.129.31.2:2001,116.202.114.157:2001,195.201.167.19:2001
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
  XGT_SEED_HOST=$seed_host \
  rake run
```

Set `MINING_DISABLED=TRUE` if you are setting up a sync/seed node. The value of `MINING_THREADS` depends on your machine. Run `ctrl-o` to save and `ctrl-x` to exit.

16. `chmod +x runXGT.sh`

17. `./runXGT.sh`
