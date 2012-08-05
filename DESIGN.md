Algorithm:

* Scan directories for executable files.
* Execute each file with no options.
* Each file prints to stdout either a fact book or an index.
* Send the dependent values to the executables that provided an index.

If the program printed an index then it may be executed again with options of
the values of the facts that book depends on. If the value is just a scalar it
will be sent in the form (e.g. the string "foo" is sent as the value foo). If
the value is a data structure, then the value will be serialized to JSON.

The executables must print to stdout a supported MIME type followed by a
newline followed by the data in the format indicated by the MIME type.

Supported MIME types:

* application/facter-book+json
* application/facter-book+yaml
* application/facter-index+json
* application/facter-index+yaml

Examples
========

## Fact book

Execute:
````
example
````

STDOUT:
````
application/facter-book+json
{
  "fact name": { "some": ["value"] },
  "second fact": 2
}
````

## Index:

Execute:
````
example-index
````

STDOUT:
````
application/facter-index+json
{
  depends: ["different fact"]
  provides: ["fact name", "another fact"]
}
````

Execute:
````
example-index "--different fact" "value"
````

STDOUT:
````
application/facter-book+json
{
  "fact name": { "some": ["value"] },
  "another fact": 2
}
````