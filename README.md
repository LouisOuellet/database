# Database Class

I found this class on https://codeshack.io/super-fast-php-mysql-database-class/. David Adams did a really good job with this class. Besides adding the fetchObject, getHeaders, get, create, save, setModified and delete methods, this class is all his work. The additional methods are there to simplify SQL Requests while also offering an entry for permissions.

## Author

David Adams - https://codeshack.io/super-fast-php-mysql-database-class/
Louis Ouellet - (the fetchObject method)

## Change Log
 * [2020-08-17] - Adding CRUD Methods
 * [2020-08-17] - Adding getHeaders Method
 * [2020-08-16] - Uploaded to GitHub

## Requirements for the Database Class
 * PHP
 * MySQL

## Testing environment
### Hardware
 * Dual-Core Intel® Core™ i5-4310U CPU @ 2.00GHz
 * Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)
 * 7.9 GB memory
 * 471.5 GB storage (SATA SSD)
### Software
 * elementary OS 5.1.7 Hera
 * Apache/2.4.39 (Unix)
 * PHP 7.3.5 (cli) (built: May  3 2019 11:55:32) ( NTS )
 * MySQL Ver 15.1 Distrib 10.1.39-MariaDB

## Usage
### Basics
```php
require_once('database.php');
$db = new Database('host','username','password','database');
```

### Example
```php
// We need to include the Database Class
require_once('database.php');

// Connect to MySQL database:
$db = new Database('host','username','password','database');

// Fetch a record from a database:
$account = $db->query('SELECT * FROM accounts WHERE username = ? AND password = ?', 'test', 'test')->fetchArray();
echo $account['name'];

// Fetch a record from a database as objects:
$account = $db->query('SELECT * FROM accounts WHERE username = ? AND password = ?', 'test', 'test')->fetchObject();
echo $account->name;

// Fetch multiple records from a database:
$accounts = $db->query('SELECT * FROM accounts')->fetchAll();

foreach ($accounts as $account) {
	echo $account['name'] . '<br>';
}

// Get the number of rows:
$accounts = $db->query('SELECT * FROM accounts');
echo $accounts->numRows();

// Get the affected number of rows:
$insert = $db->query('INSERT INTO accounts (username,password,email,name) VALUES (?,?,?,?)', 'test', 'test', 'test@gmail.com', 'Test');
echo $insert->affectedRows();

// Get the total number of queries:
echo $db->query_count;

// Get the last insert ID:
echo $db->lastInsertID();

// Close the database:
$db->close();

// Get table headers:
$db->getHeaders('accounts');

// Get record:
$db->get('accounts', 'test', 'username');

// Create record:
$account = [
	'username' => 'test',
	'password' => 'test',
	'name' => 'test',
];
$db->create('accounts', $account);

// Save record for row 1 but you can also specify the search parameter by setting a 4th parameter as the column:
$account = [
	'username' => 'test',
	'password' => 'test',
	'name' => 'test',
];
$db->save('accounts', $account, 1);

// Delete record for row 1 but you can also specify the search parameter by setting a 3th parameter as the column:
$db->save('accounts', 1);

exit;
```
