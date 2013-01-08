# 0.8 blockchain data upgrade

Submit completed tests and debug.log files to:  [Gavin Andresen](mailto:gavin@bitcoinfoundation.org)

Version tested:
{0.x.y release candidate N, or git commit}

Test environment:
  Operating system:
  Upgrading from:
  
## Bounties:

0.5 BTC : Test starting from version 0.7.2
0.5 BTC : Test starting from version 0.3.24
0.5 BTC : Test on Windows XP, NTFS filesystem
0.5 BTC : Test on Windows (any version), FAT32 filesystem 

Bounties will go to the first people who follow the instructions in TestPlanExecution.md and this test plan and
submit test results and timestamped debug.log files.

## Test Setup

1. Begin by running an old version, fully-synced on the main network.
2. Shut down bitcoind/Bitcoin-Qt, wait for it to exit completely.
3. Backup your wallet.dat (if it contains any bitcoins; better safe than sorry!)
4. Remove [data directory](https://en.bitcoin.it/wiki/Data_directory) debug.log

## Tests

### Upgrade

Download and install test binaries from the latest successful pull-tester build; you will find a link to
the last pull-tester build in [pull request 2099](https://github.com/bitcoin/bitcoin/pull/2099).

(or, if you are able, build binaries yourself)

1. Note how much disk space is being used by the bitcoin data directory.
2. Run the new bitcoind/Bitcoin-Qt binary.

EXPECT (all tests except for FAT32 filesystem):

1. blktree/ subdirectory created in bitcoin data directory
2. small (less than 1GB) increase in disk space usage
3. startup takes longer than ususual (blocks are re-indexed)
4. but startup does not take hours (blocks are not re-downloaded)

PASS/FAIL


EXPECT (FAT32 or other filesystem that does not support hardlinks):

1. blktree/ subdirectory created in bitcoin data directory
2. same experience as a brand-new user: entire blockchain is re-downloaded

PASS/FAIL


### Downgrade

1. Shut down the new bitcoind/Bitcoin-Qt, wait for it to completely exit
2. Run the old version of bitcoind/Bitcoin-Qt

EXPECT:

1. Quick startup
2. Old version is synchronized to blockchain from where it last exited

PASS/FAIL
