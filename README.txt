Local build
===========

1. Adjust maven properties and target configuration in

      ./pom.xml

2. Adjust repository location in

      pepper-target/pepper-target.target

3. Run test to build OSGI bundles

      mvn -P osgi package

4. Install OSGI bundles into your local Maven repository

      mvn -P osgi install

5. Run test to build Eclipse bundles

      mvn -P eclipse package

6. Install Eclipse bundles into your local Maven repository

      mvn -P eclipse install


Frequently asked questions
==========================

How can I adjust the version of the Pepper core modules?
--------------------------------------------------------

Change maven properties

      pepper.core.version
      pepper.core.version.osgi

in ./pom.xml. If you are building against a snapshot version use

      pepper.core.version       x.y.z-SNAPSHOT
      pepper.core.version.osgi  x.y.z.SNAPSHOT

As of Pepper version 1.1.6 timestamped versions are not possible because the
entry bundle-version in the manifest files of the Pepper bundles is not
timestamped.


How can I add a special Pepper import/export module?
----------------------------------------------------

1. Add the module as Maven dependency with the dependency management section of

      ./pom.xml

2. Add the module as Maven dependency with the dependency section of

      pepper-feature-modules/pom.xml
      pepper-repository/pom.xml

3. Add the module as plugin to the Eclipse feature definition file

      pepper-feature-modules/feature.xml



How can I add the source of a special Pepper import/export module?
------------------------------------------------------------------

1. Make sure the module is contained in the Pepper Modules Feature (see above)

2. Define a new property containing the version of the Pepper module in

      ./pom.xml

   and a corresponding OSGI version property; cf. the Maven properties

      pepper.module.paula.version
      pepper.module.paula.version.osgi

3. Add a new Maven module which builds the source of the Pepper module as OSGI
   bundle; cf.

      pepper-plugin-module-paula-source/pom.xml

4. Include this Maven module in the <modules> section of the profile OSGI in

      ./pom.xml

5. Add the new Maven module as Maven dependency with the dependency section of

      pepper-feature-modules-source/pom.xml
      pepper-repository/pom.xml

   Use the group id, the artifact id and the version of the new Maven module,
   not those of the original pepper module.

6. Add the module as plugin to the Eclipse feature definition file

       pepper-feature-modules-source/feature.xml


How can I add a bundle required from the target platform?
---------------------------------------------------------

Add this bundle to pepper-target/pepper-target.target either as feature or
individual bundle.

