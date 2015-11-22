SonarQube on OpenShift
=========================

``SonarQube`` is a popular code profiler and dashboard that excels when used along
a Continuous Integration engine.

More information can be found at http://www.sonarqube.org

Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

For a detailed step by step introduction on how to set up SonarQube 5.2 and Jenkins with Github projects see also [here](https://itaffinity.wordpress.com/2015/11/17/building-github-projects-with-jenkins-maven-and-sonarqube-5-2-on-openshift/).

Create a DIY application. If you may add a PostgreSQL cartridge.

    rhc app create sonar diy-0.1 postgresql-9.2

Add this upstream SonarQube quickstart repo

    git rm -r diy .openshift misc README.md
    git remote add upstream -m master https://github.com/worldline/openshift-sonarqube.git
    git pull -s recursive -X theirs upstream master

Push the repo upstream to OpenShift

    git push

Head to your application at:

    http://sonar-$yourdomain.rhcloud.com

Default Credentials
-------------------
<table>
<tr><td>Default Admin Username</td><td>admin</td></tr>
<tr><td>Default Admin Password</td><td>admin</td></tr>
</table>

To give your new SonarQube site a web address of its own, add your desired alias:

    rhc app add-alias -a sonar --alias "$whatever.$mydomain.com"

Then add a cname entry in your domain's dns configuration pointing your alias to $whatever-$yourdomain.rhcloud.com.

