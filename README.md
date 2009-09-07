Google App Engine support for JavaScript
========================================

A port of the Python AppEngine API to JavaScript.

* Homepage: [http://nitrojs.org/](http://nitrojs.org/)
* Source & Download: [http://github.com/gmosx/nitro/](http://github.com/gmosx/appengine/)
* Documentation: [http://nitrojs.org/docs](http://nitrojs.org/docs)
* Mailing list: [http://groups.google.com/group/nitro-devel](http://groups.google.com/group/nitro-devel)
* Issue tracking: [http://github.com/gmosx/nitro/issues](http://github.com/gmosx/appengine/issues)
* IRC: #nitrojs on [irc.freenode.net](http://freenode.net/)    


Component status
----------------

This library is under construction but usable. Substantial parts of the Python API are converted.

* google/appengine/api/memcache: 80% (usable)
* google/appengine/api/urlfetch: 80% (usable)
* google/appengine/api/mail: 60% (usable)
* google/appengine/api/images: 20% (usable)
* google/appengine/api/users: 10%
* google/appengine/ext/db: 50% (usable, expect minor API changes)
* google/appengine/ext/db/forms: 20% (expect API changes)


Datastore
---------

The Python ext/db api is supported. The API is slightly different to better fit JavaScript:

    var Category = exports.Category = function(term, label, category) {
	    this.term = term;
	    this.label = label;
	    this.category = category;
	    this.__key__ = Category.key(this);
    }

    Category.model = new db.Model(Category, "Category", {
	    term: new db.StringProperty(),
	    label: new db.StringProperty(),
	    category: new db.ReferenceProperty({referenceClass: Category})
    });

    Category.key = function(obj) {
        return db.key("Category", obj.term);
    }

    var c = new Category("news", News");
    c.put();
    var key = ...
    var c1 = Category.get(key);
    var c2 = Category.getByKeyName("news");
    var categories = Category.all().limit(3).fetch();


Example
-------

For an example of the usage of this library have a look at the [blog-gae](http://github.com/gmosx/blog-gae) example.


Credits
-------

George Moschovitis <george.moschovitis@gmail.com>


License
-------

Copyright (c) 2009 George Moschovitis, http://gmosx.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER 
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
