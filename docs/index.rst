.. ssdb-py documentation master file, created by
   sphinx-quickstart on Mon Dec 30 16:01:21 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to ssdb-py's documentation!
===================================

What is SSDB?
-------------

SSDB is a fast NoSQL database for storing big list of billions of elements.

SSDB is stable, production-ready and is widely used by many Internet companies
including QIHU 360. It's repository is https://github.com/ideawu/ssdb


About ssdb-py
-------------

ssdb-py is a ssdb python client like redis. It provides two types of
connection-pool and a group of functions of ssdb.

It's repository is https://github.com/wrongwaycn/ssdb-py


Quickstart
----------

.. code-block:: python

   >>> from ssdb import SSDB
   >>> import time
   >>> ssdb = SSDB(host='127.0.0.1', port=8888)
   >>> ssdb.multi_set(set_a='a', set_b='b', set_c='c', set_d='d')
   4
   >>> ssdb.multi_set(set_x1='x1', set_x2='x2', set_x3='x3', set_x4='x4')
   4
   >>> ssdb.multi_set(set_abc='abc', set_count=10)
   2
   >>> ssdb.multi_hset('hash_1', a='A', b='B', c='C', d='D', e='E', f='F',
   ...                 g='G')
   7
   >>> ssdb.multi_hset('hash_2',
   ...                 key1=42,
   ...                 key2=3.1415926,
   ...                 key3=-1.41421,
   ...                 key4=256,
   ...                 key5='e',
   ...                 key6='log'
   ...                )
   6
   >>> ssdb.multi_zset('zset_1', a=30, b=20, c=100, d=1, e=64, f=-3,
   ...                 g=0)
   7
   >>> ssdb.multi_hset('zset_2',
   ...                 key1=42,
   ...                 key2=314,
   ...                 key3=1,
   ...                 key4=256,
   ...                 key5=0,
   ...                 key6=-5
   ...                )
   6
   >>> ssdb.get('set_a')
   'a'
   >>> ssdb.setx('set_ttl', 'ttl', 5)
   True
   >>> ssdb.get('set_ttl')
   'ttl'
   >>> time.sleep(5)
   >>> ssdb.get('set_ttl')
   >>> 
   >>> ssdb.exists('set_a')
   True
   >>> ssdb.incr('set_count', 3)
   13
   >>> ssdb.multi_get('a', 'b', 'c', 'd')
   {'a': 'a', 'c': 'c', 'b': 'b', 'd': 'd'}
   >>> ssdb.keys('set_x ', 'set_xx', 3)
   ['set_x1', 'set_x2', 'set_x3']
   >>> ssdb.scan('set_x ', '', 10)
   {'set_x1': 'x1', 'set_x2': 'x2', 'set_x3': 'x3', 'set_x4': 'x4'}
   >>> ssdb.delete('set_abc')
   True
   >>> ssdb.hget("hash_1", 'a')
   'A'
   >>> ssdb.hexists('hash_2', 'key2')
   True
   >>> ssdb.hdecr('hash_2', 'key1', 7)
   36
   >>> ssdb.hsize('hash_1')
   7
   >>> ssdb.hlist('hash_ ', 'hash_z', 10)
   ['hash_1', 'hash_2']
   >>> ssdb.hscan('hash_1', 'a', 'g', 10)
   {'b': 'B', 'c': 'C', 'd': 'D', 'e': 'E', 'f': 'F', 'g': 'G'}
   >>> ssdb.zget("zset_1", 'b')
   20
   >>> ssdb.zset("zset_1", 'z', 1024)
   True
   >>> ssdb.zset_exists('zset_2')
   True
   >>> ssdb.multi_zget('zset_1', 'a', 'b', 'c', 'd')
   {'a': 30, 'c': 100, 'b': 20, 'd': 1}
   >>> ssdb.zkeys('zset_1', '', 0, 200, 3)
   ['g', 'd', 'b']
   >>> ssdb.zscan('zset_1', '', 0, 200, 10)
   {'g': 0, 'd': 1, 'b': 20, 'a': 30, 'e': 64, 'c': 100}
   >>> ssdb.zrscan('zset_1', 'a', 30, -1000, 3)
   {'b': 20, 'd': 1, 'g': 0}
   >>> ssdb.zrank('zset_1','d')
   2
   >>> ssdb.zrrange('zset_1', 0, 4)
   {'c': 100, 'e': 64, 'a': 30, 'b': 20}
      

Content
-------

.. toctree::
   :maxdepth: 2
  
   connection
   code


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

