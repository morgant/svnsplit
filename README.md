# svnsplit
by Morgan Aldridge <morgant@makkintosshu.com>

## OVERVIEW

`svnsplit` is a wrapper around `svnadmin` & `svndumpfilter` which simplifies the process of splitting portions of a Subversion repository out into a new repository. It allows specifying inclusions and exclusions, incl. supporting globbing to make it easier to hone in on exactly what you want.

## USAGE

There are two required parameters: `-i <input-repo-uri>` and `-o <output-repo-path>`; `-i` being the input repository URI for a local repository and `-o` being the path & name to the new repository to create.

Optional commands are: `include <path> [...]` and `exclude <path> [...]`, each accepting an arbitrary number of repository-relative paths to either include or exclude. These repository-relative paths support globbing ('?', '*', etc) for matching files and paths, if wrapped in double quotes.

*Important considerations:*

* `svnsplit` currently only operates on local repositories, which must be specified with a full `file://` URI.
* While the `include` and `exclude` commands and paths can be specified together and in either order, inclusions always supersede exclusions in the order of operations. After all, you can't exclude something that hasn't been included!
* When including only a subdirectory, make sure to include any parent directories to ensure that the repository can be created correctly. It doesn't know to create parent directories which you've excluded, directly or indirectly. 

It is suggested to use the `-v` option for verbose output.

## EXAMPLE

    svnsplit -v -i file:///path/to/input/repo -o new-repo include trunk trunk/some/path exclude trunk/some/other-path

## LICENSE

`svnsplit` is licensed under the MIT license. See [LICENSE](LICENSE).