email-peryton
=============
### Simply wrap various templating libs and node-mailer into a single package for ease of reuse

[![Build Status](https://drone.io/github.com/mvhenten/peryton/status.png)](https://drone.io/github.com/mvhenten/peryton/latest)

Introduction
------------

These are the templating systems supported: 

- [Swig](https://github.com/paularmstrong/swig)
- [Jade](https://github.com/visionmedia/jade)

Examples
--------

##### Swig

```javascript
    var Email = require('peryton'),
        email = Email.create({
        template: 'file.html',
        transport: Email.Transport({
            service: 'SES',
            auth: CONFIG.AmazonSES
        }),
        engine: Email.Swig({
            config: {
                cache: process.env['NODE_ENV'] === 'production' ? 'memory' : false,
            },

            filters: { smurf: function(str){ return str.replace(/\w+/g,'smurf') } }
        }),
    });


    email.send( to, from, subject, locals, function( err, email ){
        // check err
        // etc.
    });
```

##### Jade

```javascript
    var Email = require('peryton'),
        email = Email.create({
        template: 'file.jade',
        transport: Email.Transport({
            service: 'SES',
            auth: CONFIG.AmazonSES
        }),
        engine: Email.Jade({
            config: {
                cache: process.env['NODE_ENV'] === 'production' ? 'memory' : false,
            },

            mixins: { smurf: function(str){ return str.replace(/\w+/g,'smurf') } }
        }),
    });


    email.send( to, from, subject, locals, function( err, email ){
        // check err
        // etc.
    });
```

