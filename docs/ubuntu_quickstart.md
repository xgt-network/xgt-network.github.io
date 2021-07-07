## Steps to Run Linux Build

1. Download Ubuntu Desktop 20.04 LTS ISO from the [Ubuntu website](https://ubuntu.com/download/desktop)

2. Create a VM with the image from step 1 (process depends on your machine - not covered here)

3. Download/copy .sh file from [this link](https://gist.githubusercontent.com/obskein/fbfd8d87660297e8be7edf01921ab7a8/raw/4a1b03b31814fd96890cfb7401bbf60a8c657a90/install_xgt.sh)

4. `chmod +x install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located

5. `./install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located
	- this will take 10-15 minutes

6. `sudo apt install ruby-full`

7. `sudo gem install xgt-ruby`

8. `cg xgt`

9. `rake configure`

10. `rake make`
	- this will take 10-15 minutes

13. `XGT_WALLET=XGT-Wallet-Address MINING_THREADS=4 XGT_WIF=Your-XGT-Recovery-Private-Key XGT_RECOVERY_PRIVATE_KEY=Your-XGT-Recovery-Private-Key XGT_WITNESS_PRIVATE_KEY=Your-XGT-Recovery-Private-Key XGT_SEED_HOST=98.33.76.100:2001,xgt.rag.pub:2001,xgt2.rag.pub:2001,45.138.27.42:2001,68.129.31.2:2001,116.202.114.157:2001,195.201.167.19:2001 rake run`

#### _Steps 11-13 must be run from within the xgt directory_
#### If you encounter problems with `rake run`, try `rake clean` and then repeat steps 11-13
