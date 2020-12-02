<!doctype html>

<title>CodeMirror: ProtoBuf mode</title>
<meta charset="utf-8"/>
<link rel=stylesheet href="../../doc/docs.css">

<link rel="stylesheet" href="../../lib/codemirror.css">
<script src="../../lib/codemirror.js"></script>
<script src="protobuf.js"></script>
<style>.CodeMirror { border-top: 1px solid #ddd; border-bottom: 1px solid #ddd; }</style>
<div id=nav>
  <a href="https://codemirror.net"><h1>CodeMirror</h1><img id=logo src="../../doc/logo.png"></a>

  <ul>
    <li><a href="../../index.html">Home</a>
    <li><a href="../../doc/manual.html">Manual</a>
    <li><a href="https://github.com/codemirror/codemirror">Code</a>
  </ul>
  <ul>
    <li><a href="../index.html">Language modes</a>
    <li><a class=active href="#">ProtoBuf</a>
  </ul>
</div>

<article>
<h2>ProtoBuf mode</h2>
<form><textarea id="code" name="code">
package addressbook;

message Address {
   required string street = 1;
   required string postCode = 2;
}

message PhoneNumber {
   required string number = 1;
}

message Person {
   optional int32 id = 1;
   required string name = 2;
   required string surname = 3;
   optional Address address = 4;
   repeated PhoneNumber phoneNumbers = 5;
   optional uint32 age = 6;
   repeated uint32 favouriteNumbers = 7;
   optional string license = 8;
   enum Gender {
      MALE = 0;
      FEMALE = 1;
   }
   optional Gender gender = 9;
   optional fixed64 lastUpdate = 10;
   required bool deleted = 11 [default = false];
}

</textarea>
  <textarea id="code2" name="code2">
syntax = "proto3";
package tutorial;

import "google/protobuf/timestamp.proto";
option java_package = "com.example.tutorial";
option java_outer_classname = "AddressBookProtos";
option csharp_namespace = "Google.Protobuf.Examples.AddressBook";

message Person {
  string name = 1;
  int32 id = 2;  // Unique ID number for this person.
  string email = 3;

  enum PhoneType {
    MOBILE = 0;
    HOME = 1;
    WORK = 2;
  }

  message PhoneNumber {
    string number = 1;
    PhoneType type = 2;
  }

  repeated PhoneNumber phones = 4;

  google.protobuf.Timestamp last_updated = 5;
}

// Our address book file is just one of these.
message AddressBook {
  repeated Person people = 1;
}
service Test {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
  rpc SayHelloAgain (HelloRequest) returns (HelloReply) {}
}</textarea>
</form>
    <script>
      var editor = CodeMirror.fromTextArea(document.getElementById("code"), {});
      var editor = CodeMirror.fromTextArea(document.getElementById("code2"), {});
    </script>

    <p><strong>MIME types defined:</strong> <code>text/x-protobuf</code>.</p>
