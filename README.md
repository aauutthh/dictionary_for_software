# dictionary_for_software
 This is a dictionary project , and it can be used for generate a dictionary for [dictd](http://dict.org)  which  is an opensource service for dict .   
 "dictd  is  a  server  for  the  Dictionary Server Protocol (DICT), a TCP transaction based query/response protocol that allows a client to access dictionary definitions from a set of natural language dictionary databases."    
 this introduction is from man page(man dictd)    

## generation
 run this:  
 `cat sdict_src.txt | dictfmt -c5 -s "a dictionary for software" --utf8 sdict`    
 will generate two files .    
 `sdict.dict` : dict file   
 `sdict.index` : index file   
 one can compress `sdict.dict` to `sdict.dict.dz` by execute `dictzip sdict.dict` , either can be accepted by dictd.    

## how to use   
1. install and config

 ```
 sudo apt-get install dictd dict-gcide
 sudo perl -pi -e 's/^(server localhost)/\1 { port 8089 }/' /etc/dictd/dict.conf
 sudo perl -pi -e 's/^(listen_to 127.0.0.1)/\1\nport 8089 /' /etc/dictd/dictd.conf
 ```

 append the below text to `/var/lib/dictd/db.list`

 ```
 database sdict
  {
   data  /data/dictd/dicts/sdict.dict
   index /data/dictd/dicts/sdict.index
 }
 ```

1. start

 `sudo service dictd start`

1. reload

 `sudo service dictd reload`
 
1. search by client

 `dict version`
 
