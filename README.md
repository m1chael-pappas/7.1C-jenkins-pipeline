# 7.1C Jenkins Pipeline

A seven stage declarative Jenkins pipeline covering build, test, analysis, security scanning and deployment.
Every stage echoes the task it performs and the tool that would perform it, so the pipeline runs anywhere without a build toolchain.

## Stages

| Stage | Task | Tool |
| --- | --- | --- |
| Build | Compile and package the application into a deployable artefact | Maven |
| Unit and Integration Tests | Verify individual components, then verify they work together | JUnit, Selenium |
| Code Analysis | Find bugs, code smells and standards violations | SonarQube |
| Security Scan | Scan dependencies and code for known CVEs | OWASP Dependency-Check |
| Deploy to Staging | Push the packaged artefact to a staging server | AWS CodeDeploy to EC2 |
| Integration Tests on Staging | Run end to end tests against staging | Postman/Newman, Selenium |
| Deploy to Production | Push the verified artefact to production | AWS CodeDeploy to EC2 |

## Running it

Create a Jenkins pipeline job, point it at this repository with `Pipeline script from SCM`, branch `main`, script path `Jenkinsfile`.

The `triggers` block polls SCM every two minutes, so a push to `main` starts a build on its own.

Set the same `H/2 * * * *` schedule under Poll SCM in the job configuration as well. Jenkins only
registers a Jenkinsfile `triggers` block once a build has parsed it, so a job relying on the block
alone will not poll until you have run it by hand. Setting it in both places arms polling from build
one.

A build that polling started says `Started by an SCM change` at the top of its console output, rather
than `Started by user`. That line is how you tell the trigger fired on its own.
