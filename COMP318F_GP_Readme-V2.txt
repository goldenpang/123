## Database structure
id : login name(string)
pwd: login password(string)
name: account name(string)
admin: did this user have admin perrmission?(true/false)
phoneNo: phone number(string)
englishScore: score(number)
chineseScore: score(number)
mathScore: score(number)
################################################################

## Exist Account
[Admin] id: tony, pwd: 123
[non-admin] id: test, pwd: test
[non-admin] id: tom, pwd: tom123
################################################################

## [Create] Need Admin Account, create Student File and store score
e.g.>>  curl -X POST http://localhost:8099/api/create -H "Content-Type: application/json" -d '{"id":"tony","pwd":"123","newid":"bob","newpwd":"bob123", "name":"Bob Leung","phone":"1234567890","eng":4,"chi":4,"math":4}' 
Result: Admin "tony" create a new Student File id called "bob", named "Bob Leung", which login password is "bob123", 
its phone number is "1234567890", English score is "4", Chinese Score is "4", Math score is "4"


##  [Read] Need Admin Account, Check all Student File, sort(0: ascend, 1: descend), default is sort=0
e.g.>>  curl -G "http://localhost:8099/api/read/all" --data-urlencode "id=tony" --data-urlencode "pwd=123" --data-urlencode "sort=1" 
Result: Show all non-admin account information, sort descending


##  [Read] Need Admin Account, Check specfic Student File
e.g.>>  curl -G "http://localhost:8099/api/read/one" --data-urlencode "id=tony" --data-urlencode "pwd=123" --data-urlencode "targetid=test"
Result: show the specfic account "test"'s information


##  [Read] Any Account, check account information
e.g.>>  curl -G "http://localhost:8099/api/read" --data-urlencode "id=tony" --data-urlencode "pwd=123" 
Result: show the account "tony"'s information


## [Update] Need Admin Account, edit account information
e.g.>>  curl -X PUT http://localhost:8099/api/updateScore -H "Content-Type: application/json" -d '{"id":"tony","pwd":"123","targetid":"test","math":"4"}' 
Result: Account "test"'s math score is update to "4"


## [Update] Need Admin Account, update English and Chinese score
e.g.>>  curl -X PUT http://localhost:8099/api/updateScore -H "Content-Type: application/json" -d '{"id":"tony","pwd":"123","targetid":"test","eng":"5","chi":"4"}' 
Result: Account "test"'s english score and math score are update to "5" and "4"


## [Update] Any Account, edit account information(name, phone number)
e.g.>>  curl -X PUT http://localhost:8099/api/updateInfo -H "Content-Type: application/json" -d '{"id":"tony","pwd":"123","pno":"99999999", "name":"tony2"}' 
Result: Account "tony" phone number is update to "99999999"


## [Delete] Need Admin Account, delete user
e.g.>>  curl -X DELETE http://localhost:8099/api/delete -H "Content-Type: application/json" -d '{"id":"tony","pwd":"123","targetid":"bob"}'
Result: Account "bob" got deleted
