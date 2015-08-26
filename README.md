# Flask-Cassandra

Flask-Cassandra provides an application-level connection to an Apache Cassandra database.  This connection can be used to interact with a Cassandra cluster.

Flask-Cassandra requires both Flask and the [Datastax Python Driver for Apache Cassandra](https://github.com/datastax/python-driver) to be installed.  This driver will be installed automatically when installing via `pip` or when running `setup.py install`.

## Installation

The easiest way to use the extension is to install it from [PyPI](https://pypi.python.org/pypi/Flask-Cassandra) using pip:
```sh
$ pip install flask-cassandra
```

You can also install the extension directly from source.

```sh
$ python setup.py install
```

## Use

This is an example flask app that reads from a Cassandra cluster.

```python
from flask import Flask
from flask_cassandra import CassandraCluster

app = Flask(__name__)
cassandra = CassandraCluster()

app.config['CASSANDRA_NODES'] = ['cassandra-c1.terbiumlabs.com']  # can be a string or list of nodes
app.config['CASSANDRA_KEYSPACE'] = 'pythonista' # default keyspace


@app.route("/cassandra_test")
def cassandra_test():
    session = cassandra.connect("monty_python") # connect to the monty_python keyspace, it not specified will use the default keyspace.
    cql = "SELECT * FROM sketches LIMIT 1"
    r = session.execute(cql)
    return str(r[0])

if __name__ == '__main__':
    app.run()

```

## Contributions

If you would like to extend the functionality of the extension, pull requests are most welcome.
