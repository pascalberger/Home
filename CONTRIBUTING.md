# How do I, as an Addin Author, transfer a repository to the Organisation?

Moving a repository into this organisation is a very simple process, but it does involve a couple hoops.  It is not possible to move a repository directly into the organisation, unless you are an owner of the organisation.

As a result, the easiest way to move a repository into this organisation is to first transfer the repository to a member of the Cake Team, and from there, they will move it into the Cake Contrib organisation.
Please [start a new discussion](https://github.com/cake-build/cake/discussions) to initiate the process.

Once that request has been made, the following process will be followed:

* If the original maintainer of the repo hasn't been invited to the `cake-contrib` organisation, an invite will be sent out
* If a team has not been created in the Organisation for the original maintainer of the repo, one will be created using the convention `Team <First Name>`
* Repository will be transferred from Team Member account to `cake-contrib` Organisation, and added to the `Team` and `Team <First Name>` teams
* Once the transfer is complete, go to the settings of the repository and click on `Collaborators & teams` tab
* Give Admin permission to all Teams
* Remove all collaborators, as they should now be included as teams
* Check with the original owner if they want to use the standard labels for issues in this repository.  If they do, run the label creation tool
* Go to AppVeyor
* If this was a new user invited to the organisation, create a matching role for that user and map the GitHub Team to that role
* Add a new AppVeyor Project for the new repository
* Run the permission sync tool
  * If this was a new user added to the organisation, you will need to run the tool for all projects
  * If this was an existing user adding a new project, you will only need to run the tool for one project
* Check the permissions to make sure that they are filled out
* Create environment variable for `WYAM_DEPLOY_REMOTE` and add value (similar to existing projects i.e. `https://github.com/cake-contrib/Cake.Hg`)
* Go to coveralls.io and add new project using `cake-contrib` account
* Create environment varialbe for `COVERALLS_REPO_TOKEN` and copy in value from above step
* Inform user of process being complete

# What permissions will I, as an Addin Author have, once I move it to this organisation?

The bottom line is, we want you, as the original Addin creator, and potential continued maintainer, to have the exact same permissions that you had when you created the repository in the first place.

To this end, the following things will happen:

* A new GitHub Team will be created for yourself
* Any repositories that you are going to be maintaining will be added to this Team with full admin permissions
* An AppVeyor Project will be created for the new repositories in the organisation
* An AppVeyor Role will be created which will map to the new GitHub Team
* This AppVeyor Role will be provided with the correct permissions to access each AppVeyor Project
* The necessary settings will be added to the AppVeyor project to allow notifications to be sent via the official Cake Contrib communication channels

# Tracking Addin's, Modules and Recipes

Due to the growing number of Addins, Modules and Recipes that are available, we have  implemented an automated process to track the current status of each of these. This process runs twice a day (at noon and midnight UTC) and generates a [summary report](https://github.com/cake-contrib/Home/blob/master/Audit.md).

The generated report contains information such as:

* the fact that the addin/module/recipe actually exists
* a link to the github project (or the NuGet package if unable to determine the project URL)
* whether the addin is compatible with the latest release of Cake
* information about the maintainer
* whether the cake-contrib user has been added as a co-maintainer to the NuGet packages
* whether the addin repository has been moved to the Cake Contrib organisation
* whether the addin follows all recommendations

This process also automatically generates and updates the YAML file for each addin that is subsequently used to generate the publicly available documentation for a given addin. This YAML used to be manually maintained by the addin author but this is no longer necessary since the automation takes care of it. However, it's important to note that the content of the YAML file is generated based on the information contained in the addin's package nuspec file. This means that addin authors must ensure the information in their nuspec files is accurate.
