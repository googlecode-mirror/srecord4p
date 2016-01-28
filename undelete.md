# Introduction #

undelete() method is used for deleting record form Salesforce.

# Usage #
You must specify Id with property or parameter.
```
$result = Sobject_Account::neu()->undelete('xxxxxxxxxxxxxxxx');
```
or
```
$account = new Sobject_Account();
$account->Id = 'xxxxxxxxxxxxxxxx';
$result = $account->undelete();
```