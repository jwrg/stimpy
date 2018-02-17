#stimpy

Provisioning tool for fast prototyping and multi-system dotfile storage

The following is not so much a readme but is a design specification at present

##Command line switches

__sync/push__
_-s (-S) or -u (-U) remote\_location_
Push a config file set as per the user's .config/stimpyconf file, which must
be configured for sync to work.  The .config/stimpyconf file must at minimum
have each dotfile location specified.

When differences are found, the user confirms the changes with a diff.  When
all changes have been approved, the changes are pushed to remote directory.

__no to all__
_-n (-N)_
Don't to a diff, just push/pull new files and keep all old files as they are
presently.

__yes to all__
_-y (-Y)_
Don't do a diff, just push/pull all new files and all changes non-
interactively.

__pull/provision__
_-p (-P) remote\_location_
Specifying -p brings down a config file set from a specified remote 
directory and installs it as per the .stimpyfc file in the directory.

When differences are found, the user confirms the changes with a diff.  When
all changes have been approved, the changes are installed to the local system.

If there is a default location specified in the user's .config/stimpyconf
file, the parameter can be omitted.

__remote directory__
_-d (-D) fileset\_name_
Specifying -d looks for a subdirectory with that system name for a file
set and .stimpyfc file.  This is a way of grouping multiple potentially
related configs at a single remote location.

The top level dotfile set is the default, nameless set.  It gets pulled
when there is no hostname specified using the -d switch.

If there is a default directory specified in the user's .config/stimpyconf
file, the parameter can be omitted.

## Other design considerations

* Every folder in the remote location, including the top level nameless set
has a .stimpyfc file present.  It indicates where each file in the fileset
is to be installed on the system being provisioned.

* Will need a way to resolve filename collisions, i.e., using local directory
names as the remote file name (e.g., etc.portage.make.conf).

* Later:  Include an interactive (with a non-interactive mode) script for
provisioning gentoo systems from the minimal environment.
