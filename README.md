<p align="center">
  <img src="https://raw.githubusercontent.com/finagle/finch/master/finch-logo.png" width="360px" />
</p>

Finch is a thin layer of purely functional basic blocks atop of [Finagle](http://twitter.github.io/finagle) for 
building composable REST APIs. Its mission is to provide the developers simple and robust REST API primitives being as close as possible to the bare metal Finagle API.

Modules
-------

Finch uses multi-project structure and contains of the following _modules_:

* [`finch-core`](core) - the core classes/functions
* [`finch-json`](json) - the lightweight and  immutable JSON API
* [`finch-demo`](demo) - the demo project
* [`finch-jawn`](jawn) - the JSON API support for the [Jawn](https://github.com/non/jawn) library
* [`finch-argonaut`](argonaut) - the JSON API support for the [Argonaut](http://argonaut.io/) library
* [`finch-jackson`](jackson) - the JSON API support for the [Jackson](http://jackson.codehaus.org/) library

Installation 
------------
Every Finch module is published at Maven Central. Use the following _sbt_ snippet ...

* for the _stable_ release:
 
```scala
libraryDependencies ++= Seq(
  "com.github.finagle" %% "[finch-module]" % "0.4.0"
)
```

* for the `SNAPSHOT` version:

```scala
resolvers ++= Seq(
  "Sonatype OSS Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots"
)

libraryDependencies ++= Seq(
  "com.github.finagle" %% "[finch-module]" % "0.5.0-SNAPSHOT" changing()
)
```

Quickstart
----------
This quick start example is built with the `0.4.0` version of both `finch-core` and `finch-json`.

```scala
def hello(name: String) = new Service[HttpRequest, HttpResponse] {
  def apply(req: HttpRequest) = for {
    title <- OptionalParam("title")(req)
  } yield Ok(Json.obj("greetings" -> s"Hello, ${title.getOrElse("")} $name!"))
}

val endpoint = Endpoint[HttpRequest, HttpResponse] {
    // routes requests like '/hello/Bob?title=Mr.'
    case Method.Get -> Root / "hello" / name => hello(name)
  }
}
```

Documentation
-------------
 * A comprehensive documentation may be found in the [`docs.md`](docs.md) file in the root directory
 * The latest Scaladoc is [here](http://finagle.github.io/finch/docs/#io.finch.package)

Contacts
--------

* Use a Gitter room for questions like _"How do I ..."_ [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/finagle/finch?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Adopters
--------
* [Konfettin](http://konfettin.ru)
* [JusBrasil](http://www.jusbrasil.com.br)
* [Sabre Labs](http://sabrelabs.com)
* *Submit a pull-request to include your company/project into the list*

License
-------

Licensed under the **[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)** (the "License");
you may not use this software except in compliance with the License.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

----
[![Build Status](https://travis-ci.org/finagle/finch.svg?branch=master)](https://travis-ci.org/finagle/finch)
[![Coverage Status](https://coveralls.io/repos/finagle/finch/badge.svg?branch=master)](https://coveralls.io/r/finagle/finch?branch=master)
