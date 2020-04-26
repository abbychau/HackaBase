# HackaBase

The last DBaaS you need.

## Usage:

### Initialization / migration
```php
<?php 
include('vendor/autoload.php'); // or include('HackaBase.php');
define("SECRET_TOKEN","9877f9924811c69ec16e08db02553630");
$tableSampleData = [
  'users'=>[
    ['name'=>'Peter', 'age'=>30, 'mass'=>71.1, 'parent_id'=>3],
    ['name'=>'John', 'age'=>33, 'mass'=>73.1, 'parent_id'=>1],
    ['age','mass','parent_id']//indexes
  ],
  'parents'=>['name'=>'Tifa', 'age'=>66, 'mass'=>40, 'slogan'=>'I love my dad']
];
$hbConn->AutoMigrate(
$tableSampleData, 
hb::RELATIONAL_DB, //Storage type, can be //hb::DOCUMENT_STORE //hb::COLUMN_STORE
SECRET_TOKEN,
true //create table structure only or load data as well
); 
```

### HTTP(s)

This is for quick prototyping and light-weight usage:
```
$hbConn = hb::CreateHttpConnection(SECRET_TOKEN);
$result = $hbConn->DbAr("SELECT u.name, p.name FROM users u, parents WHERE u.parent_id = p.id WHERE u.id = :id", ['id'=>$_GET['id']]);
print_r($result[0]);
```

### TCP
This is for heavy and prolong operations: (good for production)
```
<?php
$hbConn = hb::CreateTcpConnection(SECRET_TOKEN);
$result = $hbConn->DbAr("SELECT u.name, p.name FROM users u, parents WHERE u.parent_id = p.id");
print_r($result[0]);
```
