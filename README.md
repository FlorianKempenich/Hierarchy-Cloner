# Hierarchy
[![Travis](https://img.shields.io/travis/FlorianKempenich/hierarchy.svg)](https://travis-ci.org/FlorianKempenich/hierarchy) [![PyPI](https://img.shields.io/pypi/v/hierarchy.svg)](https://pypi.org/project/hierarchy/)

Hierarchy is a simple tool that allows you to clone and maintain an entire hierarchy of Git repository in _one single command_:
```
$ hierarchy
```
> TODO: Add picture of `hierarchy` in action

## Quick-Start

1. **Install**
   ```bash
   $ pip install hierarchy
   ```

2. **Create the _Hierarchy_ file**
   ```bash
   $ nano ~/.hierarchy
   ```

   > _Sample Hierarchy File_
   > ```yaml
   > repos:
   >   - path: ~/Dev/CliTools
   >     url: git@github.com:FlorianKempenich/Hierarchy.git
   >     
   >   - path: ~/Dev/CliTools
   >     url: git@github.com:FlorianKempenich/kata.git
   >     
   >   - path: ~/Dev/CliTools/DevOps
   >     url: git@github.com:FlorianKempenich/ansible-droplet.git
   >     
   >   - path: ~/Dev/HomeAutomation
   >     url: git@github.com:FlorianKempenich/Appdaemon-Test-Framework.git
   >     name: appdaemontestframework
   > ```

3. **Run _Hierarchy_**
   ```bash
   $ hierarchy
   ```
   * _Hierarchy_ will clone all the repositories at the specified location
   * If a repo already exists at the specified location,  _Hierarchy_ will pull  
     the latest changes (WIP)
   * If a repo contains local modifications or has some un-pushed commits,  
     the repo will be skipped and a warning will be emitted (WIP)

## _Hierarchy_ file structure

The _Hierarchy_ file represents the flattened hierarchy of all the git repository to clone and maintain. 

It consists of a list of entries, under the key `repos`, each representing a repository to clone.
```yaml
repos:
  - REPO_TO_CLONE_1
 
  - REPO_TO_CLONE_2
  
  - REPO_TO_CLONE_3
```
Each repository has the following structure:
```yaml
url: "URL of the project. The same used to clone the repository with `git clone`"
path: "The local path where to clone the repository. It can contain `~` to represent HOME"
name: "OPTIONAL - A name to override the default repository name when cloning"
```

**The repository will be cloned at:** `path/name`  
If no `name` is provided, the repository name will be used.


A sample _Hierarchy_ file might look like this:
```yaml
repos:
  - path: ~/Dev/CliTools
    url: git@github.com:FlorianKempenich/Hierarchy.git
    
  - path: ~/Dev/CliTools
    url: git@github.com:FlorianKempenich/kata.git
    
  - path: ~/Dev/CliTools/DevOps
    url: git@github.com:FlorianKempenich/ansible-droplet.git
    
  - path: ~/Dev/HomeAutomation
    url: git@github.com:FlorianKempenich/Appdaemon-Test-Framework.git
    name: appdaemontestframework
```

## Options

* ### `-f` / `--file HIERARCHY_FILE`
  A hierarchy file to use.  
  _Default:_ `~/.hierarchy`
  
* ### `-v` / `--verbose`
  Enable verbose mode
  
* ### `--help`
  Show help



---
## Work In Progress

- [x] Allow for `~` in the `path`
- [x] Create directories if do not exist
- [ ] Clone with all submodules
- [ ] If directory exists and not empty:
    - [ ] Is not same repo => Skip and notify user (ERROR)
    - [ ] Is not repo => Skip and notify user (ERROR)
    - [ ] Is correct repo:
        - [ ] Has no local modifications and up to date with remote =>
            - [ ] Update (pull)
            - [ ] Update with all submodules
        - [ ] Has local modifications => Skip and notify user (WARN)
        - [ ] Is not up to date with remote => Skip and notify user (WARN)


