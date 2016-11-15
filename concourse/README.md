# Concourse Directory Contract

### Directory Structure
The Concourse directory should contain this README and three sub-directories only:

* pipelines
* tasks
* scripts

##### Pipelines Directory
There should be four pipelines in this directory:

* `pipeline.yml` the pipeline that compiles, tests, and produces installers from the master branch of gpdb.
* `dev_pipeline.yml` a safe-to-duplicate version of `pipeline.yml` which saves artifacts to dev buckets.
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

### The Concourse Deployment
There is a `gpdb` team in the [Concourse instance](http://gpdb.ci.pivotalci.info/).
This team should only have the `gpdb_master`, `gpdb_pr`, and `concourse_upgrade` pipelines.

There is a `dev` team which is where developer pipelines should live.

### Creating Your Own Pipeline
Many developers want to create their own copies of the master pipeline.
To accommodate this without naming confusion, workload instability, and artifact collision we have the following solution:

1. All developer pipelines should live in the `dev` team.
1. Duplicate the `dev_pipeline` so that the artifacts are placed in a safe bucket.

To duplicate the pipeline do something like the following:
``` bash
fly -t gpdb login -n dev
fly -t gpdb get-pipeline -p dev_pipeline > /tmp/pipeline.yml
# update gpdb_src with your desired source
fly -t gpdb set-pipeline -c /tmp/pipeline.yml -p NEW_PIPELINE_NAME
```

### Updating This README
Changes should be proposed to this contract with a PR.
