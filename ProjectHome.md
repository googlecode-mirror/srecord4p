sRecord is a PHP5 data access library for Salesforce and Force.com.<br />
It wraps [Salesforce PHP Toolkit](http://wiki.developerforce.com/index.php/PHP_Toolkit) and makes it useful, easy to develop application like ActiveRecord of RoR.

  * sRecord provides intuitive interface with method-chain design pattern.
  * sRecord manipulates child-parent relationship and parent-child relationship easily.
  * sRecord generates entity class, which makes possible to write method in entity class.
  * sRecord is designed to develop on Eclipse PDT, on help with code assist functionality of IDE.

# Summary #

## Query single record ##
```
$account = Sobject_Account::neu()->find('0018000000UoDxpAAF');
echo ("<td>{$account->Id}</td>");
echo ("<td>{$account->Name}</td>");
echo ("<td>{$account->Phone}</td>");
```

## Query multiple records ##
```
$records = Sobject_Account::neu()->eq('Type','Prospect')->select();
forecah ($records as $record) {
    echo ("<td>{$record->Id}</td>");
    echo ("<td>{$record->Name}</td>");
    echo ("<td>{$record->Phone}</td>");
}
```

## Child-parent relationship ##
```

$account = Sobject_Account::neu()
    ->join('Owner','Id, Username')
    ->join('CreatedBy','Username')
    ->find('0018000000UoDxpAAF');
echo ("<td>{$account->Id}</td>");
echo ("<td>{$account->Name}</td>");
echo ("<td>{$account->Owner->Username}</td>");
echo ("<td>{$account->CreatedBy->Username}</td>");

```

## Parent-child relationship ##
```

$records = Sobject_Account::neu()
    ->child('Contacts', 'Id, Name')
    ->child('Cases', 'Id, Reason')
    ->starts('Name', 'G')
    ->select('Id, Name');
forecah ($records as $record) {
    echo ("<td>{$record->Id}</td>");
    echo ("<td>{$record->Name}</td>");
    echo ("<td>{$record->Cases[0]->Reason}</td>");
    echo ("<td>{$record->Cases[1]->Reason}</td>");
    echo ("<td>{$record->Contacts[0]->Name}</td>");
    echo ("<td>{$record->Contacts[1]->Name}</td>");
}

```

## Create ##
```

$account = Sobject_Account::neu();   // same as new Sobject_Account();
$account->Name = 'Scott';
$result = $account->create();
if (! $result) {
    print_r($account->getErrors());
}

```

## Update ##
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

# Documents #
  * [setup](setup.md)
  * [query](query.md)
  * [relationship](relationship.md)
  * [create](create.md)
  * [update](update.md)
  * [upsert](upsert.md)
  * [delete](delete.md)
  * [undelete](undelete.md)
  * [createAll updateAll upsertAll deleteAll](SchemaMethod.md)

# Downloads #
available at "Download" tab

# Contacts #
  * email: ｉｎｆｏ＠ｈｏｎｅｓｔｙｗｏｒｋｓ．ｊｐ
  * twitter: @miztaka or hash tag #srecord

# Todo #
  * Validation according to SObject description.
  * Options for list type columns.





