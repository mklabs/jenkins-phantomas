# jenkins-phantomas

Phantomas integration with Jenkins CI server. Exposes convenient scripts
to run phantomas and generate JSON & HTML reports.

## Installation

    npm i mklabs/jenkins-phantomas

## Scripts

Options and configurable parts are all set with environment variables.

### phantomas-job

    $ JENKINS_URL="http://192.168.33.12:8080" JENKINS_JOBNAME="phantomas-job" node_modules/.bin/phantomas-job

Creates a new job on remote Jenkins, with name `phantomas-job` based on
`config.xml` job template.

- `JENKINS_URL` Jenkins root URL
- `JENKINS_JOBNAME` The name of the job to create

Created jobs expect the following plugins to be installed:

- Tap plugin: https://wiki.jenkins-ci.org/display/JENKINS/TAP+Plugin
- Parameterized trigger plugin: https://wiki.jenkins-ci.org/display/JENKINS/Parameterized+Trigger+Plugin

### phantomas-run

    $ ./node_modules/.bin/phantomas-run

Used by `config.xml` job template. Runs phantomas on preconfigured URLs,
generating JSON results.

### phantomas-format

    $ ./node_modules/.bin/phantomas-format

Aggregates JSON results into a single JSON file (array of JSON results)
for downstream jobs to consume.

### phantomas-html

    $ ./node_modules/.bin/phantomas-html ./results/$BUILD_NUMBER

Lookups build results directory for screenshots and HAR file. Generates
an `index.html` file with filmstrip screenshots and HAR using
[har-viewer](http://www.softwareishard.com/har/viewer/)

HTML file generated in `./results/$BUILD_NUMBER`. harviewer files and
application are copied to `./results/harviewer`.

### phantomas-metrics

    $ ./node_modules/.bin/phantomas-metrics ./metrics.json

Generates `metrics.json` file, data per metrics / url and `metrics.html`
file to show graph for each metric. Uses highcharts and bootstrap.
