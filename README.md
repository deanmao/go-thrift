Thrift Package for Go
=====================

WARNING
-------

*This package is a work in progress.*

Overview
--------

So why another thrift package? While the existing one
([thrift4go](https://github.com/pomack/thrift4go/)) works well, my philosophy
is that interface should match the language.

As an example, Go already has the idea of a thrift transport in the
ReadWriteCloser interfaces.

Another design decision was to keep the generated code as terse as possible.
The generator only creates a struct and the encoding/decoding is done through
reflection. Annotations are used to set thrift ID for a field and options such
as 'required'.

Example struct:

    type User struct {
        Id        int64    `thrift:"1,required"`
        Name      string   `thrift:"2"`
        PostCount int32    `thrift:"3,keepempty"`
        Flags     []string `thrift:"4"`
    }

Types
-----

Most types map directly to the native Go types, but there are some
quirks and limitations.

* Go supports a more limited set of types for map keys than Thrift
* To use a set define the field as []type and provide a tag of "set":

        StringSet []string `thrift:"1,set"`

* Unsigned types aren't supported. Thrift only has signed types. Could
  encode/decode unsigned types as their signed counterparts, but I
  decided against that for now.
