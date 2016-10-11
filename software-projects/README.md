Software Projects
=================

These guidelines apply to all software projects.
There are definitely cases where some of it doesn't apply - so do things differently, if there are good reasons for it.

Hosting
-------
We host software projects on GitHub.

Licensing
---------
Open source projects are released under the MIT license, copyright Cargo Media.

Versioning
----------
Projects are versioned using [Semantic Versioning](http://semver.org/).
Dependencies are included with pessimistic "approximately greater than" version constraints (Composer: `~x.y.z`, Rubygems: `~> x.y.z`).

Testing, CI and CD
------------------
Projects have a **test suite** that covers the main functionality of the program.
Tests are running **automatically for every pull request** on Travis.

Releasing of new versions happens automatically (for example when a new tag is pushed) with a [Travis deployment](https://docs.travis-ci.com/user/deployment/).

Documentation
-------------
The *README* of the project covers at least the following topics:
- **Description**: Describe the purpose of the program, and the problem it solves.
- **Installation & Configuration**: Describe how the program is installed, configured and run.
- **Development**: Describe how to install the development tree of the program, how to run tests, and how to release a new version.
