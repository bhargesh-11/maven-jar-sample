## GitHub Action Workflow
A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered manually.

* Within the repository, create the `.github/workflows/` directory to store the workflow files.
* In the `.github/workflows/` directory, create a new workflow file called `main.yml`.
* Workflow file:
  * Name the workflow as `BDDS-Server` as it will appear in the Actions tab of the GitHub repository.
  * `on: workflow_dispatch` allows you to run the workflow manually from the Actions tab.
  * `jobs:` Groups together all the jobs that run in the BDDS-Server workflow. 
  * Configure the job to run on `ubuntu-latest` runner which is a GitHub hosted runner.
  * Each item nested under `steps` section is a separate action or shell script.
  * Checkout your repository code onto the runner with `actions/checkout@v2`
  * Setup OpenJDK using `actions/setup-java@v1` with `java-version 11`
    * Use `run` keyword to execute a command on the runner. We are using `mvn` as the build command.
  * Create a release using `actions/create-release@v1`.
    * `id:` The ID using which the release can be identified.
	* `GITHUB_TOKEN:` This token is provided by Actions, you do not need to create your own token.
	* `tag_name:` The name of the tag for this release.
    * `release_name:` The name of the release.
    * `body:` Text describing the contents of the release.
  * Upload release asset using `actions/upload-release-asset@v1`
    * `GITHUB_TOKEN:` This token is provided by Actions, you do not need to create your own token.
	* `upload_url:` The URL for uploading assets to the release, this will come from actions/create-release@v1 GitHub Action.
	* `asset_path:` The path to the asset you want to upload.
	* `asset_name:` The name the file gets as an asset on a release.
	* `asset_content_type:` The content-type of the asset you want to upload. See the supported Media Types [here](https://www.iana.org/assignments/media-types/media-types.xhtml)
* To run the workflow navigate to the Actions tab of the GitHub repository you will then see a `Run workflow` button for **BDDS-Server** enabling you to easily trigger a run.
* Select the branch and then click on `Run workflow`.
* You can see whether a workflow run is in progress, complete, success, failure or cancelled, from the workflow run page.
* If your workflow run fails, you can see which step caused the failure and review the failed step. You can also see the time it took for each step to run.
