# Introduction #
You can specify child-parent relationship, parent-child relationship with using join() and child() method. To specify relationship, Salesforce relationship names are used.

# Child-parent relationship #
join() method is used to specify child-parent relationship like bellow.
```
$account = Sobject_Account::neu()
    ->join('Owner','Id, Username')
    ->find('0018000000UoDxpAAF');
```
(select() is also available in similar to this.)<br />
In this case, Account is a child of Owner.You can get Owner.Username like bellow.
```
echo ($account->Owner->Username);
```
"Owner" in this case is not a name of SObject, but a relationship name for Account -> Owner.

The specification of child-parent relationship can be nestable.
```
$records = Sobject_Case::neu()
    ->join('Contact')
    ->join('Contact.Account')
    ->starts('Contact.Account.Name', 'G')
    ->order('CaseNumber')
    ->select();
foreach ($records as $record) {
    echo ($record->Contact->Account->Name);
}
```

# Parent-child relationship #
child() method is used to specify parent-child relationship. For example,
```
$records = Sobject_Account::neu()
    ->child('Cases', 'Id, reason', 'reason = ?', 'Feedback')
    ->select('Id, Name');
```
generates SOQL like bellow.
```
SELECT Id, Name, (SELECT ID, reason FROM Cases WHERE reason = 'Feedback') FROM Account
```
You can get child objects through relationship name.
```
$account = Sobject_Account::neu()
    ->child('Cases', 'Id, reason', 'reason = ?', 'Feedback')
    ->find('xxxxxxxxxxxxxxxx');
foreach ($account->Cases as $case) {
    echo ($case->reason);
}
```
