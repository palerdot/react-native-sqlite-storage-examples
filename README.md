# react-native-sqlite-storage-examples
```javascript
```
### Examples
```javascript
// import
import SQLite from 'react-native-sqlite-storage'
// init db
let db = SQLite.openDatabase({name: 'test.db', createFromLocation : "~example.db", location: 'Library'}, successCB, errorCB)
// sample execution
db.transaction((tx) => {
  tx.executeSql('SELECT * FROM test', [], (tx, results) => {
      console.log("Query completed");

      // Get rows with Web SQL Database spec compliance.

      var len = results.rows.length;
      for (let i = 0; i < len; i++) {
        let row = results.rows.item(i);
        console.log(`Record: ${row.name}`);
        this.setState({record: row});
      }
    });
});
```

### Promise based example
```javascript
import SQLite from 'react-native-sqlite-storage';
SQLite.DEBUG(true);
SQLite.enablePromise(true);

let db;

// echo test to check for db?
SQLite.echoTest()
  .then(() => {
    // success; OPENING db?
    SQLite.openDatabase({name : "test5.db", createFromLocation : "~/db/andrew.db"}).then((DB) => {
        db = DB;
    }).catch((error) => {
        console.log(error);
    });
  })
  .catch(error => {
    // error in handling db
  });
  
// now db has the dqlite db handle
// perform normal query
db.executeSql('SELECT 1 FROM Version LIMIT 1')
  .then(() => {})
  .catch(error => {})
// performing transactions
db.transaction('transaction query')
  .then((tx) => {})
  .catch(error => {})
```
