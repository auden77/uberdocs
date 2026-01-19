# umbrellatree protocol
## Forms
There are two forms of an umbrellatree:

  1. class
  2. instance

### umbrellatree Classes
An umbrellatree class consists of a directory tree and a manifest file at the root of the directory tree. The directory tree defines paths whose leaf nodes represent a placeholder for git repositories. It is essentially a structure within which git repositories can be organized, and which serves as a template for umbrellatree instances. The root path is a git repository and contains a .git directory; however, it does not contain any submodules and does not have a .gitmodule file. Class umbrellatrees may or may not contain a repository in their leaf nodes.
The root directory of an umbrellatree class contains a manifest file, `umbrellatree.manifest`, which identifies repositories which can be included in instance umbrellatrees. `umbrellatree.manifest` has the following format:
```
parent_repo_url umbrellatree_path [space-separated list of instances which follow this entry]
```
umbrellatree classes should preferably use the following naming convention:
```
umbrellatree.<name_which_identifies_the_umbrellatree_project>-<generation>.class
```
The generation should be at least a 3-place zero-padded number which identifies the backup priority of the class. In other words, an umbrellatree class with a generation of 000 would be considered the most-canonical version of that class. While lesser-canonical versions can be updated before those with a higher priority, efforts should be made to prefer updating the highest-canonical (000) class.
umbrellatree classes can be cloned by running a script which does the following:
  1. clone the umbrellatree manifest file
  2. iterate through the manifest and create the directory structure for every entry, then clone any repositories contained within the umbrellatree directory tree

### umbrellatree Instances
An umbrellatree instance is a git repository which has a directory structure which, either partially or completely, mirrors the directory structure of a class umbrelllatree.

umbrellatree instance names should have the following format:
```
umbrellatree.<name_which_identifies_the_umbrellatree_project>-<instance_identifier>.instance
```
The manifest should be cloned from the umbrellatree class, preferring the highest canonical-priority. The repositories defined in the manifest can be cloned into their corresponding paths within the directory tree. Leaves (repositories) of the tree can be added to the instance by adding the instance identifier to the corresponding entry in the manifest, according to the requirements of that instance.
A file named `.umbrellatree` should be put in the root directory and should contain the following key-value pairs:
```
instance_name=<instance_name>
```
A script can be run to create and update the umbrellatree instance by doing the following:
  1. ensure directory paths for all desired leaf nodes exist
  2. clone all desired repositories according to the url in the manifest, using `umbrellatree` as the upstream remote identifier

To create a new leaf node (repository) in that instance and include it in the class umbrellatree, the following must be done:
  1. create a new directory in the instance for the new repository
  2. create the new repository in the instance and commit
  3. create a corresponding entry in the manifest
  4. commit the manifest change and push to the umbrellatree class
  5. push the newly-created repository to the umbrellatree class
  6. set the url of the repository as it exists in the umbrellatree class as remote `umbrellatree`

