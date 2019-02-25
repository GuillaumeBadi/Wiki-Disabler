[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)'


# Wiki-Disabler
A simple script to automatically Disable the GitHub wikis on all repositories in an organisation.

This was created because prior to around 2015, any repositories created in GitHub, by default, had the wiki enabled, and allowed anyone to edit the wiki, even if they didn't have push/edit access to the repository. This opens up somewhat of an exploit opportunity, as it allows a malicious user to post malicious information (eg, links to malicious versions of the project) to the wiki, and exploit the fact that many people might see the wiki as a trusted source of information.

Unfortunately, GitHub doesn't expose that anyone can edit configuration option of wikis in the GitHub API, so there's no straight forward way of auditing and updating this. However, I do agree, Wiki is a term usually associated with collaboration or crowd-sourced information and it should be the readers responsibility to not believe anything written in a wiki, like in case of any phishing attempt but it is also not required to be publicly editable anyways. So, just disabling the wiki altogether achieves the same thing.

## Usage

Create a GitHub application token, and set in the environment variable:

```
export GITHUB_TOKEN=e72e16c7e42f292c6912e7710c838347ae178b4a
```

Now run the project, passing the organisation you want to disable the wikis of as an argument:

```
sbt "run YOUR_ORGANISATION"
```

The script will only disable a wiki if the following is true:

* The wiki is enabled
* The project is not archived (since you can't disable the wiki of an archived project)
* The wiki is either empty, or contains a single Home.md file containing less than 100 bytes

If last condition is not true, then the script will output a link to the wiki at the end of the run so that it can be manually checked to see if it needs the wiki or not.
