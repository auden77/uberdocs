# umbrellaTree
## Description
==can umbrellaTree instead be a specification that uses the pre-existing git submodule to achieve this?==
umbrellaTree is a way to organize and manage git repositories in a directory tree. It allows us to have a collection of git repositories, with each existing in a unique state. This can be useful when managing a large project that uses two or more repositories from disparate origins.

An unbrellaTree is a directory tree which contains any number of subdirectories. In each subdirectoy of the tree exists the potential to contain one or more git repositories, or "leaves." Each leaf, being a separate repository, can have its own remote origin, or even be an origin itself. The leaves of the tree may exist in various states.

In the root directory of the tree is a directory named ".unbrellaTree," which contains the following files: 

## .umbrellaTree directory
* `archetype` a csv file describing all potential leaves of the tree, each line containing the following information about a leaf:
  * path of leaf 
  * the preferred branch for the leaf
  * the current commit for the leaf - if the commit field is blank, then the leaf has not been pulled down from its origin

## Scripts
There also exist several shell scripts: 

* `umbrellaTree.update.sh` - runs a git update on each leaf of the tree.
* `umbrellaTree.allHeadsToLatest.sh` - traverses the tree and makes sure every leaf is up to date with its origin and preferred branch
* `umbrellaTree.identify-pending.sh` - lists every leaf that has changes that have no been committed
* `umbrellaTree.identify-lagging.sh` - lists every leaf in the tree that is behind the remote origin
* `umbrellaTree.createLeaf.sh` - creates a subdirectory and initializes a git repository for an empty leaf in the tree 
* `umbrellaTree.cloneLeaf.sh` - creates a subdirectory and clones a git repository to it

## Instance Names
umbrellaTree instances should have the following name structure:
```
umbrellaTree.<archetypal_name>.<instance_name>
```
