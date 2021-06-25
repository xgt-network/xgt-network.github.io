---
layout: default
title: Ubuntu VM Quickstart
---

# Ubuntu VM Quickstart

## Steps to Run Linux Build

1. Download Ubuntu Desktop 20.04 LTS ISO from the [Ubuntu website](https://ubuntu.com/download/desktop)

2. Create a VM with the image from step 1 (process depends on your machine - not covered here)

3. Download/copy .sh file from [this link](https://gist.githubusercontent.com/obskein/fbfd8d87660297e8be7edf01921ab7a8/raw/4a1b03b31814fd96890cfb7401bbf60a8c657a90/install_xgt.sh)

4. `chmod +x install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located

5. `./install_xgt.sh`
	- must be in the directory where `install_xgt.sh` is located
	- this will take 10-15 minutes

6. `cd xgt`
	- Navigate into newly created xgt folder

7. Edit Rakefile for the following values:
	- Line 11 - TRUE for mining or FALSE to just run a node that syncs and does not mine
		- `ENV['MINING_DISABLED'] == 'TRUE'`
		or 
		- `ENV['MINING_DISABLED'] == 'FALSE'`
	- `ENV['XGT_WALLET']` with your XGT wallet address
	- `ENV['XGT_RECOVERY_PRIVATE_KEY']` with your private key
	- `ENV['XGT_WITNESS_PRIVATE_KEY']` with your private key
	- replace line 39 with: `ENV['XGT_SEED_HOST'] || '98.33.76.100:2001'`

8. Save the updated Rakefile

9. `sudo apt install ruby-full`

10. `sudo gem install xgt-ruby`

11. `rake configure`

12. `rake make`

13. `rake run`

#### _Steps 11-13 must be run from within the xgt directory_
#### If you encounter problems with `rake run`, try `rake clean` and then repeat steps 11-13
