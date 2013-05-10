ROS for Products Workshop
=========================
The workshop took place...

Requirements
------------

Quality
~~~~~~~
 * Complexity is bad. Good software architecture is the most important
 defense against incidental complexity.
 * Track and report on code quality (e.g., with QA-C++ and dashboard)
  * Bosch has started this
 * Track and report on key performance characteristics and failure rates
   * Start with ros_comm: characterize reliability, jitter, loss, failure
   modes.

Documentation
~~~~~~~~~~~~~
 * End-to-end traceability from requirements to code

Middleware
~~~~~~~~~~
 * Efficient data distribution (optimize transport and message size)
 * Diverse data types, communication patterns, rate, and latency
  * Match publisher work to subscriber capabilities (e.g., polled topics)
 * Use off-the-shelf serialization
  * is protobuf the answer?
 * Pluggable transports
  * Keep it transparent to the developer
  * Allow for configuration of everything at runtime
  * Don't require TCP stack
   * Don't even require Ethernet
    * Build translators for other physical layers (CAN, RS485, etc.)
     * ROS-I has first example of this with SimpleMessage
  * Speak (or at least bridge to) existing application protocols
  * Support zero-copy no-serialization shared-memory transport
   * Start with one copy per publish
  * Allow existing code to live alongside new code during the long
  migration process
 * Replace XMLRPC
  * Short-term, implement on embedded systems where possible
 * Admit full implementation in ANSI C
  * Including tf?
  * To run on "bare-metal" embedded systems
 * Support (or at least allow) real-time communication
  * Need to be able to link easily and efficiently to real-time subsystem
  * Make a reference real-time ROS architecture available. Recommend that
  others follow it.
   * Is orocos-ros the starting point for this?
   * How will serialization work?
 * Improve node discovery and rediscovery
 * Guard against message loss (when needed)
 * Minimize dependencies
 * Benchmark and track performance on platforms of interest
  * Bosch has started this
 * Discover and do the right thig with different physical layers
 * Support node life-cycle management.  Make programming nodes easier with
 fewer choices.  Make life-cycle status visible externally.
  * But provide an escape hatch for those who don't want their main()
  wrapped

Tools
~~~~~
 * Model-driven development enviornment (e.g., BRIDE)
 * Fast, easy-to-use, easy-to-customize simulation
 * GUI wrappers for command-line tools
 * Standard tools for visualizing system status
 * Minimize duplication of functionality across tools
 * Provide deterministic, inspectable, verifiable launch (is my system up?)
 * Minimize dependencies
 * Snapshot running system to a static file, to be "reinflated" later,
 reproducing the same computation graph
 * Build an automatic error reporting tool (ala apport)

Packaging and installation
~~~~~~~~~~~~~~~~~~~~~~~~~~
 * Improve documentation of build process/system
 * Improve visibility of maintainership and status of packages
  * New dashboard does this, with opt-in semantics for maintainers
  * Add CI results to wiki
 * Add a backport-like mechanism for brining new stuff into a stable system
  * E.g., I want MoveIt on my Fuerte system.
 * Better/easier building from source, especially on non-Ubuntu platforms
  * Is this done already, and perhaps just not well publicized?
 * Ensure that releasing is independent from Ubuntu packaging
  * Provide tarball of code with dependency information, for use by
  packagers on any platform.
 * Follow FHS (at least on Linux)
 * Manage configuration (e.g., in /etc/ros)
  * Make configuration management accessible to non-programmers
 * Manage addition of peripherals (e.g., extend udev to distinguish between
 anonymous FTDI chips).
   * Clearpath has a potential hardware solution to this problem in the
   form of programmable FTDI serial-USB tranceivers.
 * Run (some part of) ROS on boot.  Show its status in the right place
 (e.g., on title bar/dock).
 * Manage (or at least respond to changes in) network configuration
 * One-click launchers for various parts of ROS.
 * Out-of-the-box build environment for common embedded systems 
  * Specific goal: package ROS for Linux/ARM, with support comparable to
  x86, including build/test farm
    * This has been demonstrated (by Paul Mathieu).  What's left is to
    integrate some patches and then deploy the build farm.
  * Merge embedded build environment with normal build environment,
  allowing the developer to pick the target for a build and have the right
  thing happen
 * Support OSX
  * Provide binary (e.g., dmg) packages for OSX
   * This should be possible for much of the codebase
  * Setup CI
 * Support Windows
  * Start with UIs that talk to Linux ROS system
   * Get important ones done first, e.g., rviz
  * Allow full ROS system on Windows
  * Need to make the code compile, and also allow for easy installation 
  * Setup CI
 * Support mobile device platforms (Android and iOS)
  * Start with UIs that talk to Linux ROS system
  * Add more functionality, heading toward entire ROS system
 * Support custom packaging for commercial products built on ROS

Maintenance and support
~~~~~~~~~~~~~~~~~~~~~~~
 * Longevity of release (even of ROS itself)
  * Long-term bug fixing and documentation
  * Version that is stable and patched for 2-5 years
  * Make J-turtle the first LTS?
 * Stability, both API and ABI

Security
~~~~~~~~
 * Do something about security

Legal and communication
~~~~~~~~~~~~~~~~~~~~~~~
 * Build a new ros.org landing page that is not the wiki.  Make it more
 accessible to new users, make it clear what ROS does, where it runs, what
 the features, why to use it.
 * Guarantee that code is unencumbered for given use and for
 redistribution.
 * Publicize commercial development and applications of ROS
  * Establish confidence in product managers, startup companies, VCs
  * Do case study / testimonial videos with commercial users
 * Form advisory board of commercial users.
 * Specify levels of ROS support, with accompanying logos
  * "ROS-compatible," "designed for ROS," "ROS certified"
  * Start with self certification at "ROS compatible" level
  * Move on to setting up official approval process
    * Would need to design, trademark and control access to logos/marks
    * Form certification body / committee
