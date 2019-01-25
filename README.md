# EQ-R
EMEWS Queues - R implementation

EQ-R is a Swift/T (http://swift-lang.org/Swift-T/) extension that
allows Swift/T workflows to communicate with a persistent embedded R interpreter
on a worker process via blocking queues. Using the mechanism an R model
exploration (ME) algorithm can be used to control and define an ensemble
of model runs.

File index
==========

``BlockingQueue.h``
  A queue for inter-thread communication.

``EQR.h EQR.cpp``
  The main functionality to enable EQ-R- thread and queue control
  interfaces for access from Tcl and Swift.

``EQR.i``
  The SWIG interface file for EQ-R.

``settings.template.sh``
  Contains example compilier settings for compling EQ-R.

``settings.mk.in``
  Filters into ``settings.mk`` at configure time.  This can be
  ``include`` <!--- --> by other Makefiles to obtain build settings, for
  example, to compile task code that will be called from Swift.

Spack Install
=======
* [Install Spack](https://spack.readthedocs.io/en/latest/getting_started.html)
* Set up Spack shell support, e.g., for bash 
  * ``. [path to spack]/share/spack/setup-env.sh``
* Clone the EMEWS Spack repository
  * ``git clone https://github.com/emews/spack_emews``
* Change directory into the repository
  * ``cd spack_emews``
* Add the EMEWS Spack repository to your existing Spack repository or repositories
  * ``spack repo add .``
* Install EQ/R
  * ``spack install eqr``

This will install EQ/R along with any dependencies. (Look [here](http://swift-lang.github.io/swift-t/guide.html#_spack_tips) for tips for using existing dependencies.) You will then need to point to the install location of EQ/R in your EMEWS workflow launch script. The location can be queried via:

* ``spack location --install-dir eqr`` 

Manual Build
=====

Outline
-------
``./bootstrap``

``./configure ...``

``make install``

Details
-------

Run ``./bootstrap``.  This runs ``autoconf`` and generates ``./configure``.

Then, run ``./configure``.  You can use ``./configure --help``.  Key
settings are:

* ``--prefix``: EQ.R install location. This defaults to $PWD/.. for
compatibility with EMEWS templates (https://github.com/emews/emews-lazybones-templates)
* ``--with-tcl``: Point to Tcl installation root (e.g., /usr)
* ``--with-r``: Point to R installation root (requires RInside and Rcpp packages)

Then do ``make install``.

You can do ``make clean`` or ``make distclean``.


Troubleshooting
-------
**./configure halts with "checking whether the C++ compiler works... no"**

To inspect what went went wrong, you will have to look in the generated
config.log .  Check that your compiler settings in settings.sh are correct, the library locations in particular.
