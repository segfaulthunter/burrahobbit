.. burrahobbit documentation master file, created by
   sphinx-quickstart on Mon Apr  4 14:01:59 2011.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to burrahobbit's documentation!
=======================================
:mod:`burrahobbit` is a project offering the developer persistent (immutable) data
containers that allow for cheap copies and similar time complexity to the
builtin data-structures, e.g. dictionaries and sets have O(log32 n) access
complexity. Compatibility is maintained with a wide range of Python versions:
:mod:`burrahobbit` is tested against on all versions of CPython between 2.4
and 3.3 and against PyPy 1.4.
It is heavily influenced by the persistent datastructures found in the Clojure
programming language. New datastructures will be added in following releases,
0.1 will only provide sets and dicts.
Persistent data-structures are of enormous value in multi-threaded programming
because data-structures can be assumed not to change their value, this
assuring that no other thread may interfere with one's calculation.

:mod:`burrahobbit` also has the concept of transient data-structures. A
transient data-structure is a mutable version of a persistent data-structure
that can be used if many changes are done to an objects before it is exposed
to other parts of the code (i.e. it is designed for the use where a single
function does many operations on the data-structure before exposing the
object to other parts of the code by returning it or storing it within another
data-structure). A transient copy of a persistent data-structure can be
created by calling its transient member. Operations on the transient data
structure will apply the operation on the data-structure and return it. Thus,
transient data-structures can be used equivalently to persistent ones if it is
known that the state of the data-structure before the operation is no longer
needed (which can only be known if it has not left the scope of the function
operating on it - or helper functions thereof under the *direct control* of
the developer). A transient data-structure can be converted back into a
persistent one by calling its persistent member. Please be aware that after
its persistent member has been called, a transient data-structure must not be
used any more, lest the persistent data-structure's persistence can no longer
be guaranteed. A common idiom is to insert data into a transient data-structure
and eventually returning `return structure.persistent()`, e.g.
::

   import burrahobbit
   
   def double(dct):
      new = burrahobbit.dict().transient()
      for key, value in dct:
         new = new.assoc(key, value * 2)
      return new.persistent()


Contents
--------

.. toctree::
   :maxdepth: 2
   
   dict
   set

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

