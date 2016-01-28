# Introduction #

While Srecord\_ActiveRecord#create() method is used for creating single record, Srecord\_Schema::createAll() method is used for creating multiple records at once.

# createAll #

Srecord\_Schema::createAll() creates all records with specified array of srecords.<br />
You can check the result of each object by using getState() method.
```
$a1 = new Sobject_Account();
$a1->Name = 'Scott';

$a2 = new Sobject_Account();
$a2->Name = 'Tigger';

Srecord_Schema::createAll(array($a1,$a2));

if ($a1->getState() === Srecord_ActiveRecord::STATE_SUCCESS) {
    // success
} else {
    // false
    print_r($a1->getErrors());
}

```

Other methods like updateAll, upsertAll, deleteAll and undeleteAll is similar to this.

# updateAll #
```

$records = Srecord_Account::neu()->eq('Type', 'Prospect')->select();
foreach ($records as $record) {
    $record->Type = 'Other';
}
$successAll = Srecord_Schema::updateAll($records);
if (! $successAll) {
    // handle error
}

```

# upsertAll #
```

$records = array();
for ($i=0; $i<count($_POST['extid']); $i++) {
    $extid = $_POST['extid'][$i];
    $name = $_POST['name'][$i];
    $account = new Sobject_Account();
    $account->extid__c = $extid;
    $account->Name = $name;
    $records[] = $account;
}

$successAll = Srecord_Schema::upsertAll('extid__c', $records);
if (! $successAll) {
    // handle error
}

```

# deleteAll #
```

$records = Srecord_Account::neu()->eq('Type', 'Prospect')->select();
$successAll = Srecord_Schema::deleteAll($records);
if (! $successAll) {
    // handle error
}

```

# undeleteAll #
```

$records = Srecord_Account::neu()->eq('Type', 'Prospect')->select();
$successAll = Srecord_Schema::undeleteAll($records);
if (! $successAll) {
    // handle error
}

```