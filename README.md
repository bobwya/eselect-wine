# eselect-wine
**wine.eselect** - Gentoo management module for switching between installed multislot Wine packages.

## SYNOPSIS
```
eselect wine [help|usage|version]
eselect wine deregister    [variant]...        [--force] [--verbose]    target
eselect wine list         [[variant]...|--all]
eselect wine register      [variant]...        [--force] [--verbose] [--commit=COMMIT] [--date=DATE] target
eselect wine set           [variant]           [--force]                target
eselect wine show         [[variant]...|--all]
eselect wine unset        [[variant]...|--all] [--force] [--clean]
eselect wine update       [[variant]...|--all] [--force] [--if-unset]   target
```
```
variant
    [--staging|--vanilla|--wine*]  (* default)
```
```
target
    Fully qualified wine package name and version or it's associated number (as displayed in **eselect wine list** output).
```

## DESCRIPTION
**eselect wine** - is the Gentoo eselect module command for switching between installed multislot:
* **app-emulation/wine-staging**
* **app-emulation/wine-vanilla**

package versions.
The currently active package is selectable for each wine variant.

In addition a **wine target** is used to select the currently globally active default Wine package version.
This active wine target will have symbolic links in global system paths which would directly conflict with the pre-existing **app-emulation/wine**:0 package.

This eselect module uses symbolic links in:
```
  ${EPREFIX}/usr/bin/*
  ${EPREFIX}/usr/share/applications/*
  ${EPREFIX}/usr/share/man/*
```
targeting executable, desktop and manpage files (respectively) - for the currently active package version.

Details of the installed and currently active Wine package for each wine variant are stored in global configuration files under:
```
  ${EROOT}/etc/eselect/wine
```
Records are also maintained of all the symbolic links in place for the currently active Wine packages (for each wine variant) under:
```
  ${EROOT}/etc/eselect/wine/links
```
Metadata for multislot wine packages is stored in a separate file for each package:
```
  ${EROOT}/etc/eselect/wine/${P}
```
Git commit and commit date are the only currently supported metadata fields (for use with live targets).

These metadata fields are displayed (as additional columns) by the **eselect wine list** , **eselect wine show** commands.

## ACTION: DEREGISTER
```
eselect wine deregister [option]... [variant]... target
```
Deregister a multislot Wine package with the eselect module - for the specified wine variant(s)  (**_internal use only_**).
```
option
    --force          Forcibly remove a package.
    --verbose        Print detailed information about operations being performed.
```
```
variant
    --staging        Deregister a package with wine variant 'wine-staging'.
    --vanilla        Deregister a package with wine variant 'wine-vanilla'.
    --wine*          Deregister a package with system 'wine' (* default).
```
```
target
    Fully qualified wine package name and version.
```

## ACTION: LIST
```       eselect wine list [variant]...
```
Displays an ordered list of all available wine versions - for the specified wine variant(s).
An asterisk, next to one of the listed targets, denotes the currently active wine (variant) version.
```
variant
    --all            List all available targets.
    --staging        List all available wine variant 'wine-staging' targets.
    --vanilla        List all available wine variant 'wine-vanilla' targets.
    --wine*          List all available system 'wine' targets (* default).
```
## ACTION: REGISTER
```
eselect wine register [option]... [variant]... target
```
Register a new multislot Wine package with the eselect module - for the specified wine variant(s)  (**_internal use only_**).
Metadata fields are typically only used / set for live targets.
```
option
    --commit=COMMIT  Register a Git commit SHA-1 hash (COMMIT) for the specified target (metadata field).
    --date=DATE      Register a Git commit date (DATE) for the specified target (metadata field).
    --verbose        Print detailed information about operations being performed.
```
```
variant
    --staging        Register a package with wine variant 'wine-staging'.
    --vanilla        Register a package with wine variant 'wine-vanilla'.
    --wine*          Register a package with 'wine' (* default).
```
```
target
    Fully qualified wine package name and version.```
```
## ACTION: SET
```
eselect wine set [option] [variant] target
```
Set the symbolic links for a new wine version.
May also be used to reset the symbolic links for an existing wine version.
```
option
    --verbose        Print detailed information about operations being performed.
```
```
variant
    --staging        Set only the wine variant 'wine-staging' symbolic links.
    --vanilla        Set only the wine variant 'wine-vanilla' symbolic links.
    --wine*          Set only the system 'wine' symbolic links (* default).
```
```
target
    Fully qualified wine package name and version.
```

## ACTION: SHOW
```
eselect wine show [variant]...
```
Show the active system wine version - for specified wine variant(s).
```
variant
    --all            Show the active version for wine and all variants.
    --staging        Show the active wine variant 'wine-staging' version.
    --vanilla        Show the active wine variant 'wine-vanilla' version.
    --wine*          Show the active system 'wine' version (* default).
```
## ACTION: UNSET
```
eselect wine unset [option]... [variant]...
```
Remove all previously created symbolic links - for the specified wine variant(s).
```
option
    --clean          Purge any orphaned symbolic links - associated with this module.
    --verbose        Print detailed information about operations being performed.
```
```
variant
    --all            Remove symbolic links from wine and all variants.
    --staging        Remove the wine variant 'wine-staging' symbolic links.
    --vanilla        Remove the wine variant 'wine-vanilla' symbolic links.
    --wine*          Remove the system 'wine' symbolic links (* default).
```
## ACTION: UPDATE
```
eselect wine update [option]... [variant]...
```
Sets the highest installed wine version as the active system version - for the specified wine variant(s).
```
option
    --if-unset       Reuse currently selected version if it appears valid.
    --verbose        Print detailed information about operations being performed.
```
```
variant
    --all            Update main active wine and all variants.
    --staging        Update the wine variant 'wine-staging' symbolic links.
    --vanilla        Update the wine variant 'wine-vanilla' symbolic links.
    --wine*          Update the system 'wine' symbolic links (* default).
```

