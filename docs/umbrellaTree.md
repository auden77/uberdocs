# umbrellaTree
umbrellaTree is a way to organize and manage git repositories in a directory tree.

An unbrellaTree is a directory tree which contains subdirectories. At each terminal path in the tree exists a git repository, or"leaf." 

In the root directory of the tree is a directory named ".unbrellaTree," which contains the following: 
* a list of paths to each leaf in the tree

There also exists several shell scripts: 
*`umbrellaTree.update.sh` which runs a git update on each leaf of the tree.
*`umbrellaTree.identify-pending.sh` which lists every leaf that has changes that have no been committed
*`umbrellaTree.identify-lagging.sh` which lists every leaf in the tree that is behind the remote origin
