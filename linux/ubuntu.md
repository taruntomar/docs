#install a software/package
sudo apt install 'softwarename'
ex: sudo apt install curl


#config proxy for apt
create an apt.conf file inside /etc/apt
```
Acquire::http::Proxy "http://proxy:8080";
Acquire::https::Proxy "https://proxy:8080";
```
ex:
Acquire::http::proxy  "http://10.0.0.60:3128/";
Acquire::ftp::proxy "http://10.0.0.60:3128/";
Acquire::https::proxy "http://10.0.0.60:3128/";

https://stsint.abb.com

=================================================
#extract a file
tar -xf filename.tar.bz2

#rename a file
mv filename newfilename

#remove/delete a file
sudo rm filename

#create link of a file
sudo ln -s {sourcefile} {destinationfile}

#make a file executable
chmod u+x file

#print all environment variable
env

#print a specific variable
echo $http_proxy

if you accidently delete the /etc/apt/sources.list

and generate it from 
https://repogen.simplylinux.ch