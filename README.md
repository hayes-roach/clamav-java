Simple [ClamAV](http://www.clamav.net/) Java client. See also [ClamAV REST service](https://github.com/solita/clamav-rest) which builds on top of this.

Travis CI: [![Build Status](https://travis-ci.org/solita/clamav-java.svg?branch=master)](https://travis-ci.org/solita/clamav-java)

# What is provided

Support for basic INSTREAM scanning and PING command. 

Clamd protocol is explained here:
http://linux.die.net/man/8/clamd

A REST style API and server can be found from another repository, [clamav-rest](https://github.com/solita/clamav-rest). 

# Using the client

Code is self explanatory. Something like this is the idea:

## Http Client
```
  ClamAVClient cl = new ClamAVClient("192.168.50.72", 3310); // ClamAVClient(String hostname, int port)
  byte[] reply;
  try {
    reply = cl.scan(input);
  } catch (Exception e) {
    throw new RuntimeException("Could not scan the input", e);
  }
  if (!ClamAVClient.isCleanReply(reply)) {
   throw new Exception("aaargh. Something was found");
  }
```  

## Unix Socket Client
```
  ClamAVClient cl = new ClamAVClient(unixSocket); // ClamAVClient(File unixSocket)
  byte[] reply;
  try {
    reply = cl.scan(input);
  } catch (Exception e) {
    throw new RuntimeException("Could not scan the input: " + e.getMessage());
  }

  if (!clamAVClient.isCleanReply(reply)) {
    throw new Exception("aaargh. Something was found");
  }
  
```

# License

Copyright © 2014 [Solita](http://www.solita.fi)

Distributed under the GNU Lesser General Public License, either version 2.1 of the License, or 
(at your option) any later version.

