# The Jenkins Job DSL
The Jenkins Job, DSL is a plugin in Jenkins that allows you to define jobs
in a programmatic form with minimal effort.
DSL stands for Domain Specific Language.
You can describe your jobs in Jenkins using a groovy based language.
It's a scripting language.
The Jenkins Job DSL plugin was designed to make it easier to manage jobs in Jenkins.
If you don't have a lot of jobs in Jenkins using the UI is the easiest way.
When the jobs amount grow, maintaining becomes difficult and a lot of work.
The Jenkins plugin for the job DSL solves this problem and you get a lot of extra benefits.
You can use version control with it.
You then have a history, an audit log, and an easier job restore when something goes wrong.

1 - Install the Job DSL 
You can take examples from
https://github.com/alexfbasa/jenkins-course.git

```groovy
job ('Name JOB') {
    scm {
        git('git://github.com/your_repository_name') { node -> 
            node / gitConfigName('DSL User')
            node / gitConfigEmail('jenkins-dsl@youremail.com')
        }
    }
    triggers {
        scm('H/5 * * * *') //Pull after 5mns
    }
    wrappers {
        nodejs('nodejs') //Name of the NodeJS plugin installed
                         // Manage Jenkins -> Configure Tools -> NodeJS Installation -> Name
    }
    step {
        shell('npm install')
    }
}
```
You can load the job_dsl from git. 
Create a freestyle project
Set up the git repository, under the Build option check the option Process Job DSL

In the Look on Filesystem write the file path, e.g:
job-dsl/nodejs.groovy

Now it needs to be approved for  use
-- Go to Manager Jenkins 