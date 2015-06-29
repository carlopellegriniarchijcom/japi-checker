#Release notes

# 0.2.0 (roadmap) #

  * Upgrade to asm 4.0 so it can support up to Java7.
  * Add possibility to skip dependency loading error (e.g ICU has invalid class which currently fails any validation)
  * Ant task
  * Basic JSR305 validation for Nonnull/Nullable attributes.
  * Command line client
    * support local file and URL using Common VFS.

# 0.1.4 #

  * Implemented enhancement #1
  * Added check to track value changes on serialVersionUID field.
  * Added supports to full classpath during comparaison.
  * Check method exception will now use the inheritance tree to look for incompatibilities.
  * Check for base class changes,  inheritance tree is used to check for incompatibilities.

# 0.1.3 #

  * Initial release.