# Introduction #

create() method is used for creating record to Salesforce.

# Usage #
Create instance, set property, then call create().
```
$account = Sobject_Account::neu();   // same as new Sobject_Account();
$account->Name = 'Scott';
$result = $account->create();
if ($result) {
    echo("Account was created. ID is {$account->Id}");
} else {
    echo("Account creation failed.");
    print_r($account->getErrors());
}
```
Return value is boolean. If success, Id is set to the object. If not success, you can get error objects with getErrors() method.