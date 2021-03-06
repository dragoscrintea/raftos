# raftos

[![Build Status](https://travis-ci.org/zhebrak/raftos.svg)](https://travis-ci.org/zhebrak/raftos) [![PyPI version](https://badge.fury.io/py/raftos.svg)](http://badge.fury.io/py/raftos)

Asynchronous replication framework based on [Raft Algorithm](https://raft.github.io/) for fault-tolerant distributed systems.

![](https://raw.github.com/zhebrak/raftos/master/docs/img/raft_rsm.png)

#### Install

```
pip install raftos
```

#### Register nodes on every server

```python
import raftos


raftos.register(
    # node running on this machine
    '127.0.0.1:8000',

    # other servers
    cluster=[
        '127.0.0.1:8001',
        '127.0.0.1:8002'
    ]
)
```

#### Data replication

```python
class Class:
    data = raftos.Replicated(name='data')


obj = Class()

# value on a leader gets replicated to all followers
obj.data = {
    'id': 337,
    'data': {
        'amount': 20000,
        'created_at': '7/11/16 18:45'
    }
}
```

#### In case you only need consensus algorithm with leader election

```python
if raftos.get_leader() == current_node:
    # make request or respond to a client
```
Whenever the leader falls, someone takes its place.


[Paper](https://raft.github.io/raft.pdf) & [Video](https://www.youtube.com/watch?v=YbZ3zDzDnrw)
