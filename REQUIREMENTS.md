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
* The app shall check that the repo has `uncommited changes`.
* The app shall check that the repo has `not uploaded changes`.
* The app shall be configurable with a `configuration file`.

## Inputs

* The app shall accept an input to generate a `release prefix`.
* The `release prefix` will have an string appended to the beggining of the `current tag`, separated by a `-`.
* The app shall accept an input to generate a `release suffix`.
* The `release suffix` will have an string appended to the final of the `current tag`, separated by a `-`.

## Change kind

* A `major change` shall be a string that fits this regex `^major\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `major feature` and the second capturing group value will be the `major feature description`.
* A `minor change` shall be a string that fits this regex `^minor\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `minor feature` and the second capturing group value will be the `minor feature description`.
* A `patch change` shall be a string that fits this regex `^patch\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `patch feature` and the second capturing group value will be the `patch feature description`.
* A `non-apply change` shall be a string that fits this regex `^non-apply\(([^\)]\)): (.*)$` in the commit description. The first capturing group value will be the `non-apply feature` and the second capturing group value will be the `non-apply feature description`.
* A `major feature description` shall be appended to another `major feature description` if the `major feature` is exacly the same.
* A `minor feature description` shall be appended to another `minor feature description` if the `minor feature` is exacly the same.
* A `patch feature description` shall be appended to another `patch feature description` if the `patch feature` is exacly the same.
* A `non-apply feature description` shall be appended to another `non-apply feature description` if the `non-apply feature` is exacly the same.
* The app shall generate a `current tag` from `first reachable tag` following semantic versioning rules.
* The app shall increase a `major version` of the `current tag` when a commit of the `commit chain` has some `major change` defined. If the `major version` is changed, then the `minor version` and `patch version` should be 0.
* The app shall increase a `minor version` of the `current tag` when a commit of the `commit chain` has some `minor change` defined, if the `major version` is the same as the `first reachable tag`. If the `minor version` is changed, then the `patch version` should be 0.
* The app shall increase a `patch version` of the `current tag` when a commit of the `commit chain` has some `patch change` defined, if the `minor version` is the same as the `first reachable tag`.
* The app shall maintain the same version number when a commit of the `commit chain` has some `non-apply change` defined.
* The app shall fail and log the error with the commit id, commit description and `parse error` if there is no `major changes` or `minor changes` or `patch changes` or `non-apply changes` defined in a commit of the `commit chain`.

## Changelog report

* The app shall make a `changelog report` with all the `major feature` and `major feature description`, `minor feature` and `minor feature description`, `major feature` and `patch feature description`, `non-apply feature` and `non-apply feature description` information.
* The app shall group all the `major feature` with it `major feature description` in the `major changes section` of the `changelog report`.
* The app shall group all the `minor feature` with it `minor feature description` in the `minor changes section` of the `changelog report`.
* The app shall group all the `patch feature` with it `patch feature description` in the `patch changes section` of the `changelog report`.
* The app shall group all the `non-apply feature` with it `non-apply feature description` in the `non-apply changes section` of the `changelog report`.

## Outputs

* The app shall generate a `.env` file with `first reachable tag`, `current tag`, `uncommited changes`, `not uploaded changes`, `release prefix`, `release suffix` and `changelog report` if it was configured to do so.
* The app shall generate environment variables for the current bash process with `first reachable tag`, `current tag`, `uncommited changes`, `not uploaded changes` and `changelog report` if it was configured to do so.
* The app shall generate environment variables for the current powershell process with `first reachable tag`, `current tag`, `uncommited changes`, `not uploaded changes` and `changelog report` if it was configured to do so.
* The app shall generate a `.h` file with `current tag` if it was configured to do so.
* The app shall generate a `.cs` file with `current tag` if it was configured to do so.
* The app shall return 0 if the execution was done without any problem.
* The app shall return -1 if the execution has experience any problem.

TODO 
