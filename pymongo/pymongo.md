#
Ubuntu
```
apt install mongodb-server
apt install python-pip
pip install pymongo

```

```
>>> from pymongo import MongoClient
>>> client = MongoClient('localhost', 27017)
```
MongoDB URI format:
```
>>> client = MongoClient('mongodb://localhost:27017/')
```
