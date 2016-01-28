# Introduction #

sRecord uses "Method-chain" design pattern to execute query Salesforce.<br />
It's easy to understand, intuitive and very flexible.<br />
For example, if you want to execute SOQL like bellow,
```
SELECT Account.Name, FROM Account WHERE Name LIKE '%G%' AND Owner.Username = 'sato'
```
your code with sRecord is like this.
```
$records = Sobject_Account::neu()
    ->contains('Name', 'G')
    ->eq('Owner.Username', 'sato')
    ->select('Name');
```

# sRecord method and SOQL #
This is a reference of sRecord criteria method against SOQL expression.

| **function** | **SOQL** | **sRecord method** |
|:-------------|:---------|:-------------------|
| Equals       | name = 'foo' | eq('name', 'foo')  |
| Not equals   | name != 'foo' | ne('name', 'foo')  |
| Less than    | age < '10' | lt('age', 10)      |
| Less equal   | age <= '10' | le('age', 10)      |
| Greater than | age > '10' | gt('age', 10)      |
| Greater equal | age >= '10' | ge('age', 10)      |
| Like         | name like '%foo%' | contains('name','foo') |
|              | name like 'foo%' | starts('name','foo') |
|              | name like '%foo' | ends('name','foo') |
|              | name like '%appl_%'_| where("name like '%appl_%'")_|
| includes, excludes | MSP1c includes ('AAA;BBB', 'CCC') | includes('MSP1c', 'AAA;BBB', 'CCC') or <br /> includes('MSP1c', array('AAA;BBB','CCC')) |
| Boolean      | BooleanField = TRUE | eq('BooleanField', TRUE) |
|              | BooleanField  = FALSE | eq('BooleanField', FALSE) |
| Null         | SomeField = null | eq('SomeField', null) |
|              | SomeField != null | ne('SomeField', null) |
| In           | age in ('10','20','30') | in('age', '10','20','30') or <br> in('age',array('10','20','30) <br>
<tr><td> Order        </td><td> ORDER BY name, age </td><td> order('name, age') </td></tr>
<tr><td> Limit        </td><td> LIMIT 10 </td><td> limit(10)          </td></tr>
<tr><td> Offset       </td><td> OFFSET 10 </td><td> offset(10)         </td></tr></tbody></table>

<h1>Selected column #
if you want to specify selected columns, give parameter to select() method like bellow.
```
$records = Sobject_Account::neu()
    ->contains('Name', 'G')
    ->eq('Owner.Username', 'sato')
    ->select('Id, Name');
```
if no parameter is given, all of columns are selected.

# Query result #
The return value of select() method is an array of srecord objects (Sobject\_Account for example).

# Query for single row #
While select() is used to query for multiple rows, find() is used to query for single row.
If multiple rows hit in the result of find(), find() throws Srecord\_ActiveRecordException.<br />

Usage of find() is similar to select(), exept for paramters. find() can have to parameters, first is Id of SObjects, second is selected columns.
```
// example for specifing Id

$account = Sobject_Account::neu()->find('xxxxxxxxxxxxxxxx'); // xxxxx is Id of Salesforce SObject.
```