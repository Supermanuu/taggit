# Container requirements

* The container shall be easy to use. It shall be working with a one docker line.k
* The container shall mount the repo in the `/repo` path.
* The container shall be published in docker.io registry.
* The container shall be named `supermanuu/taggit`.
* The container shall never use `supermanu/taggit:latest` to avoid people to use that tag and be more specific.
* The container shall have git installed
* The container shall use non-root user
* The container user UID shall be 1000 by default
* The container user GID shall be 1000 by default
* The container UID and GID shall be configurable

# App requirements

* The app shall be programmed in Python.
* The app shall be named `taggit`.
* The app shall iterate over the commits of the current branch from HEAD to the end, looking for the `first reachable tag`. This process shall be named `tag search process`.
* The app shall define as `commit chain` the commits that are placed between HEAD and the `first reachable tag`.
* The app shall define the `latest reachable tag` as 0.0.0 when a tag is not found in the `tag search process`.

## Change kind

* A `major change` shall be a string that fits this regex `^major\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `major feature` and the second capturing group value will be the `major feature description`.
* A `minor change` shall be a string that fits this regex `^minor\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `minor feature` and the second capturing group value will be the `minor feature description`.
* A `patch change` shall be a string that fits this regex `^patch\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `patch feature` and the second capturing group value will be the `patch feature description`.
* A `non-apply change` shall be a string that fits this regex `^non-apply\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `non-apply feature` and the second capturing group value will be the `non-apply feature description`.
* The app shall increase a `major version` when a commit of the `commit chain` has some `major change` defined
* The app shall increase a `minor version` when a commit of the `commit chain` has some `minor change` defined
* The app shall increase a `patch version` when a commit of the `commit chain` has some `patch change` defined
* The app shall maintain the same version number when a commit of the `commit chain` has some `non-apply change` defined.
* The app shall fail and log the error with the commit id, commit description and `parse error` if there is no `major changes` or `minor changes` or `patch changes` or `non-apply changes` defined in a commit of the `commit chain`.

## Changelog report

* The app shall make a `changelog report` with all the `major feature` and `major feature description`, `minor feature` and `minor feature description`, `major feature` and `patch feature description`, `non-apply feature` and `non-apply feature description` information.
* The app shall group all the `major feature` with it `major feature description` in the `major changes section` of the `changelog report`.
* The app shall group all the `minor feature` with it `minor feature description` in the `minor changes section` of the `changelog report`.
* The app shall group all the `patch feature` with it `patch feature description` in the `patch changes section` of the `changelog report`.
* The app shall group all the `non-apply feature` with it `non-apply feature description` in the `non-apply changes section` of the `changelog report`.

TODO 
