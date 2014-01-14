# Upgrading

Before talking about upgrading your Fork CMS setup, let's get into our release strategy.

## Release strategy

Each release has a version number, e.g.: 3.2.7, wherein each number has it own meaning. The first number is the super number and indicates which super version it is. Since we have performed 3 invasive rewrites of Fork CMS core code, the super number is 3.
The second number is the major release number; the third number indicates the minor release version.

Each time the third number is increased, we call it a minor release. All changes in this release will be backwards compatible. If the second number increases, it is called a major release. This means changes aren't backwards compatible: deprecated methods are removed, database changes may have been made, ...

## Upgrading Fork CMS

Minor versions are easy, you can just overwrite the changed files and everything will still work. You will have to clear the cache folders. The most important ones are: `/src/Backend/Cache/CompiledTemplates`, `/src/Backend/Cache/Locale`,  `/src/Backend/Cache/MinifiedCss`, `/src/Backend/Cache/MinifiedJs`, `/src/Frontend/Cache/CachedTemplates`, `/src/Frontend/Cache/CompiledTemplates`, `/src/Frontend/Cache/Locale`, `/src/Frontend/Cache/MinifiedCss`, `/src/Frontend/Cache/MinifiedJs`. Or you could run the tools/remove_cache which automatically cleans these folders.

Upgrading to a new major release is a bit tricky. In some cases there will be database changes, so you will have to check and execute them manually. My advice would be to reinstall your Fork CMS setup.

After upgrading, you should check if there is any missing locale (http://yoursetup/private/en/locale/analyse). If there is missing locale you can import the changed XML-files through the backend (http://yoursetup/private/en/locale/import).

## Patch files

Instead of manually overwriting all files, you can also use patch-files.

### Creating the patch files

1. Open up a terminal and navigate to your clone of Fork CMS
2. Execute the following command <small>(replace the version numbers with the actual ones)</small>: `git diff 3.2.6 3.2.7 > ~/updates.patch`

Or if you don't have a local copy, you can use https://github.com/forkcms/forkcms/compare/3.2.6...3.2.7.patch <small>(thx @ defv)</small>.

### Applying the patch files

1. Open up a terminal and navigate to your project
2. Execute the following command: `patch -p0 < updates.patch`

<small>Same logic applies here, if it is a major release, some stuff can be non-backwards-compatible.</small>

## Keeping track of changes <small>(untested)</small>

Another approach is to keep track of the changes through Git. I'm going to assume you are working with the Git-version-control system.

In your local project, you add an extra remote to the Fork CMS repository. When a new version is released you can pull the changes from the remote and merge them into your own project.

### Adding the remote

1. Add the remote by executing: `git remote add fork git://github.com/forkcms/forkcms.git`
2. Fetch the remote: `git fetch fork_upstream`
3. Create a new tracking branch: `git checkout --track -b fork fork_upstream/3.2.7`

### Pulling changes

1. Update, replace 3.2.7, with the latest version: `git fetch fork_upstream/3.2.7`

### Merging changes

1. Go back to your master/branch you are working on: `git co master`
2. Merge the changes from to tracking branch, replace 3.2.7, with the latest version: `git merge fork_upstream/3.2.7`

<small>Same logic applies here, if it is a major release, some stuff can be non-backwards-compatible.</small>
