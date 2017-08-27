# Installing XGBoost on OS X / macOS

Get Homebrew if it is not installed yet.  Indeed, this is a very useful open source installer for OSX.  Instaling it is straightforward, open a terminal, then paste and execute the instruction available on Homebrew home page. I reproduce it here for convenience:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Get gcc with open mp.  Just paste and execute the following command in your terminal, once Homebrew installation is completed.
```
brew install gcc --without-multilib    
```
This automatically downloads and builds gcc.  It can take a while, it took about 30 minutes for me.  Be patient.
Get XGBoost.  Go to where you want in your filesystem, say _directoy_.  Then type the git clone command and execute it:
```
cd directory
git clone --recursive https://github.com/dmlc/xgboost 
```
This downloads the XGBoost code into a new directory named xgboost.
Next step is to build XGBoost.  By default, the build process will use the default compilers, cc and c++, which do not support the open mp option used for XGBoost multi-threading. We need to tell the system to use the compiler we just installed.  That's the step that was missing from the installation instructions on XGBoost site. 
There are various ways to do it, here is the one I used. 
Go to where we downloaded XGBoost
```
cd <directory>/xgboost
```
Then open make/config.mk and uncomment these two lines
```
export CC = gcc
export CXX = g++
```
Depending on you g++ installaiton you may need to change the above two lines into:
```
export CC = gcc-6
export CXX = g++-6
```
We then build with the following commands.
```
cd <directory>/xgboost
cp make/config.mk .
make -j4
```
Once the build is finished, we can use XGBoost with its command line.  I am using Python, hence I performed this final step.  You may need to enter the admin password to execute it.
```
cd python-package; sudo python setup.py install
```
