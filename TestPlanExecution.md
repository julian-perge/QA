Upgrading from 0.7.2.
==

Upgrading went fine on Windows 8 x64. Although a tad long to re-index everything, I received no errors or pop-up noises.

A copy of the upgrading 0.7.2-0.8.0. log file
http://www.mediafire.com/?36ezmvodhdfd4g1
password: gavina

Downgrading from 0.8.0.
==

Downgrading also went fine on Windows 8 x64. Took about 1-2 minutes to startup, and started at 128 blocks.

A copy of the downgrade
http://www.mediafire.com/?2et32gtvxrk67k7
password: gavina


Upgrading from 0.3.24 on Windows XP NTFS
==

Upgrading went fine. No errors thrown. 

Had to get about 20k blocks because 0.3.24 wouldn't open again, even though there was a process running.

http://www.mediafire.com/?9v6v5xc40efc1f8 Upgrading log

Downgrading from 0.8.0 to 0.3.24
==

I hadn't fully indexed all 210K~ blocks, but I had blk0002 which was 900MB~. 

Upon trying to downgrade with 0.3.24, I was thrown this error

Bitcoin version 0.3.24-beta
OS version Windows XP (build 2600, Service Pack 3)
System default language is 60 English_United States.1252
Language file locale/en_US/LC_MESSAGES/bitcoin.mo (English (U.S.))
Default data directory C:\Documents and Settings\weapon-x\Application Data\Bitcoin
Bound to port 8333
Loading addresses...
dbenv.open strLogDir=C:\Documents and Settings\weapon-x\Application Data\Bitcoin/database strErrorFile=C:\Documents and Settings\weapon-x\Application Data\Bitcoin/db.log
 
 
************************
EXCEPTION: 22DbRunRecoveryException      
DbEnv::open: DB_RUNRECOVERY: Fatal error, run database recovery      
C:\Program Files\Bitcoin\bitcoin.exe in AppInit()      
 
 
 
************************
EXCEPTION: 22DbRunRecoveryException      
DbEnv::open: DB_RUNRECOVERY: Fatal error, run database recovery      
C:\Program Files\Bitcoin\bitcoin.exe in CMyApp::OnUnhandledException()



************************
Runtime Error!

Program C:\Program Files\Bitcoin\bitcoin.exe

This application has requested the Runtime to terminate it in an unusual way.
please contact the application's support team for more information.
