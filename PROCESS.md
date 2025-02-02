## Process

Notes about the process surrounding the `galaxy-importer` package, which is a dependency of projects such as:
* Automation Hub [galaxy_ng](https://github.com/ansible/galaxy_ng)
* [pulp-ansible](https://github.com/pulp/pulp-ansible)
* Community Galaxy [galaxy](https://github.com/ansible/galaxy)

#### Issues and pull requests

* Issues are located at [issues.redhat.com JIRA](https://issues.redhat.com/issues/?jql=project=AAH)
* Add a changelog entry to `CHANGES/`. Changelog filename should be the number of the JIRA issue, and the extension of `.feature`, `.bugfix`, `.doc`, `.removal`, or `.misc` - see [towncrier](https://github.com/hawkowl/towncrier#news-fragments) for descriptions of each extension. Example: `CHANGES/56.feature`. File contents should be a one line description of the change.
* At least one commit must include a reference to a Jira issue on a single line in the format of `Issue: AAH-1111`
* If Pull Request is small enough not to need a Jira issue, at least one commit must include a single line with `No-Issue`
* Please run the tests in `Makefile` or install the pre-commit hook in `hooks/pre-commit` and correct any failures prior to submitting a pull request.

#### Release steps

* Test `master` branch against `pulp-ansible` functional tests inside `galaxy_ng` development environment
* Update `galaxy_importer/__init__.py` with new version number
* Run `$ towncrier` to update `CHANGES.rst`
* Push changes under commit title `Release <#.#.#>`
* Tag the commit `v<#.#.#>`, and push the tag to trigger publish to PyPi

#### Testing in other systems

* Latest `galaxy-importer` release will get consumed into `pulp-ansible` nightly builds
* Automation Hub [JIRA AAH issues](https://issues.redhat.com/issues/?jql=project=AAH) may specify a `galaxy-importer` change and a `galaxy_ng` PR will include a new release of `galaxy-importer` for testing by QE
* Community Galaxy [galaxy](https://github.com/ansible/galaxy) importer issues will include a `galaxy` PR with new release of `galaxy-importer`, and get tagged for QE
