# Concourse Directory Contract

### Directory Structure
The Concourse directory should contain this README and three sub-directories only:

* pipelines
* tasks
* scripts

##### Pipelines Directory
There should be four pipelines in this directory:

* `pipeline.yml` the pipeline that compiles, tests, and produces installers from the master branch of gpdb.
* `dev_pipeline.yml` a safe to duplicate version of `pipeline.yml` which only compiles and runs test on the given source.
* `pr_pipeline.yml` which compiles and tests pull requests.
* `concourse-upgrade.yml` which uses Concourse to upgrade itself.

##### Tasks Directory
All task yamls should live in this directory.
If a task file is not referenced in the `pipelines` directory it is considered abandoned and can be removed.

There are some exceptions to this rule.
Please do not create any more exceptions, and remove these as the occasion arises:

* `package_tarball.yml` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `test_with_planner.yml` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `test_with_orca.yml` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `build_with_orca.yml` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)

##### Scripts Directory
All script files should live in this directory.
If a script file is not referenced in any of the directories it is considered abandoned and can be removed.

There are some exceptions to this rule.
Please do not create any more exceptions, and remove these as the occasion arises:

* `cpplint.py` is being used by codegen
* `package_tarball.bash` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `builds/` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `test_gpdb.py` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)
* `build_gpdb.py` is being used by [a gporca pipeline ](https://github.com/greenplum-db/gporca/blob/master/concourse/pipeline.yml)

### Updating This README
Changes should be proposed to this contract with a PR.
