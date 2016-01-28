# Introduction #

update() method is used for updating record to Salesforce.

# Usage #
Set new values to properties, then call update().<br />
When you want to set null to properties, use fieldnull() method or specify first parameter (array of field names to set null) of update().
```
$account = new Sobject_Account();
$account->Id = '0018000000UoDxpAAF';
$account->Name = 'Tigger';
$account->fieldnull('ParentId');
$result = $account->update();
if (! $result) {
    print_r($account->getErrors());
}
```

# updateEntity #
While update() does not update empty properties, updateEntity() updates all properties of the object. (Empty properties are set to null.)<br />
It is usefull to update selected object.
```
$account = Sobject_Account::neu()->find('0018000000UoDxpAAF');
$account->Name = 'Tigger';
$account->ParentId = NULL;
$result = $account->updateEntity();
```