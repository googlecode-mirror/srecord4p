# Introduction #

upsert() method is used for creating/updating record to Salesforce.
You must specify `external ID column` at the first parameter.

# Usage #
The example below upserts record where 'JyugyoinBangoc' is '123456';
```
$extid = '123456';
$j = new Sobject_Jyugyoin__c();
$j->Name = "Test Member";
$j->JyugyoinBango__c = $extid;
$j->Age__c = 30;
$result = $j->upsert('JyugyoinBango__c');
```
Return value is boolean. If success, Id is set to the object when object was created. If not success, you can get error objects with getErrors() method.