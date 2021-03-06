===========
MongoEngine
===========
:Info: MongoEngine is an ORM-like layer on top of PyMongo.
:Author: Harry Marr (http://github.com/hmarr)
:Forked by : Anish Menon (http://github.com/anishmenon)

.. image:: https://secure.travis-ci.org/MongoEngine/mongoengine.png?branch=master
  :target: http://travis-ci.org/MongoEngine/mongoengine
  
.. image:: https://coveralls.io/repos/MongoEngine/mongoengine/badge.png?branch=master 
  :target: https://coveralls.io/r/MongoEngine/mongoengine?branch=master

About
=====
MongoEngine is a Python Object-Document Mapper for working with MongoDB.
Documentation available at http://mongoengine-odm.rtfd.org - there is currently
a `tutorial <http://readthedocs.org/docs/mongoengine-odm/en/latest/tutorial.html>`_, a `user guide
<https://mongoengine-odm.readthedocs.org/en/latest/guide/index.html>`_ and an `API reference
<http://readthedocs.org/docs/mongoengine-odm/en/latest/apireference.html>`_.

Installation
============
If you have `setuptools <http://peak.telecommunity.com/DevCenter/setuptools>`_
you can use ``pip install git+git://github.com/anishmenon/mongoengine.git``

Dependencies
============
- pymongo 2.5+
- sphinx (optional - for documentation generation)

Examples
========
Some simple examples of what MongoEngine code looks like::

    class BlogPost(Document):
        title = StringField(required=True, max_length=200)
        posted = DateTimeField(default=datetime.datetime.now)
        tags = ListField(StringField(max_length=50))

    class TextPost(BlogPost):
        content = StringField(required=True)

    class LinkPost(BlogPost):
        url = StringField(required=True)

    # Create a text-based post
    >>> post1 = TextPost(title='Using MongoEngine', content='See the tutorial')
    >>> post1.tags = ['mongodb', 'mongoengine']
    >>> post1.save()
    

    # Create a link-based post
    >>> post2 = LinkPost(title='MongoEngine Docs', url='hmarr.com/mongoengine')
    >>> post2.tags = ['mongoengine', 'documentation']
    >>> post2.save()
    
    >> TextPost.objects.latest('id') # This one will return the latest TextPost instance by id
    >> TextPost.objects.latest('posted') # This one will return the latest TextPost instance by Date

    
    
    # Iterate over all posts using the BlogPost superclass
    >>> for post in BlogPost.objects:
    ...     print '===', post.title, '==='
    ...     if isinstance(post, TextPost):
    ...         print post.content
    ...     elif isinstance(post, LinkPost):
    ...         print 'Link:', post.url
    ...     print
    ...

    >>> len(BlogPost.objects)
    2
    >>> len(HtmlPost.objects)
    1
    >>> len(LinkPost.objects)
    1

    # Find tagged posts
    >>> len(BlogPost.objects(tags='mongoengine'))
    2
    >>> len(BlogPost.objects(tags='mongodb'))
    1
    

Tests
=====
To run the test suite, ensure you are running a local instance of MongoDB on
the standard port, and run: ``python setup.py test``.






Community
=========
- `MongoEngine Users mailing list
  <http://groups.google.com/group/mongoengine-users>`_
- `MongoEngine Developers mailing list
  <http://groups.google.com/group/mongoengine-dev>`_
- `#mongoengine IRC channel <http://webchat.freenode.net/?channels=mongoengine>`_
