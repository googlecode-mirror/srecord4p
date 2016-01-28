# Introduction #

  1. Unzip archive
  1. Deploy Partner WSDL file
  1. Edit config.php
  1. Generate entity class
  1. Now ready to use it !

# Details #

## Unzip archive ##
Unzip archive somewhere.
```
$ unzip srecord-x.x.x.zip
$ ls srecord
bin lib test
```

## Deploy Partner WSDL file ##
Deploy Partner WSDL file to the directory "lib/wsdl".<br />
To generate your WSDL, login to Salesforce and go to Setup -> App Setup -> Develop -> API.<br />
Right click "Generate Partner WSDL" and save it to your directory as "partner.wsdl".

## Edit config.php ##
Edit "lib/config.php" and set your username, password, securityToken, wsdlPath.
```
Srecord_Schema::$username = 'salesforceusername';
Srecord_Schema::$password = 'salesforcepassword';
Srecord_Schema::$securityToken = 'salesforcesecuritytoken';
Srecord_Schema::$wsdlPartner = dirname(__FILE__)."/wsdl/partner.wsdl";
```

## Generate entity class ##
To generate entity class, execute "bin/generator.php".
```
$ cd bin
$ php generator.php
```
If success, SObject entity class was created in "lib/sobject" and "lib/sobjectdef".<br />
When Salesforce SObject definition has changed, just execute generator.php again to synchronize SObject definition.

## Now ready to use it ! ##
Now you are ready to use SObject entity class.<br />
In your php file, you just have to include "lib/config.php".
```
<?php

require_once "path/to/lib/config.php"

$account = new Sobject_Account(); // you can use generated entity class.

...

?>
```

