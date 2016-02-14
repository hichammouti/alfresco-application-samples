

# What are the Purchase Request Samples #

The "Purchase Request" modules are a sample project that should demonstrate how to easily map a typical business procedure like the creation of a procurement approval (in a very simplified manner) to the Alfresco Repository and Alfresco Share.
The "Purchase Request" project maps the whole process
starting with data entry via a Share form, to the automated creation of an physcial order document and the approval of the purchase request through a simple review and approve workflow.

## Target audience and purpose ##

The whole project is considered to be a starting point to help new developers and integrators with different aspects of the Alfresco and Share customization and to demonstrate how to solve typical challenges that always come up during the learning phase like :
**How do I start a workflow from my java implementation code?** How to I work with policies and behaviours?
**How do I dynamically create a content from a Share UI?
...**

The whole project is and will be work in progress as I still has some rough edges but I will constantly add functionality and round down this edges. Feel free to make suggestions improvement and for new functionality.

## Project Structure ##

The project of two artifacts a repository and a share artifacts that can be deployed as simple jar files. To ease the development and to have a clear seperation on development level, the whole sample application has been split into two seperate projects.

The **Purchase Request Repository artifact** that contains:
  * The content model defining a PurchaseRequest content type.
  * Some behaviour for the custom content type. The behaviour triggers the creation of a request number, triggers the creation of the binary request form and starts the workflow if an assignee has been selected.
  * The approval workflow definition including a java code to start workflows from a behaviour.
  * A simple webscript that creates a "Procurement" folder within the actual share site.

The **Purchase Request Share artifact** contains:
  * The custom content types form configuration (create and edit mode)
  * A dashlet to trigger the content creation

# Installation and Configuration #

_Both artifacts are mavenized so maven and some Alfresco specific prerequisites are required to build deployable repository and share artifacts._

  1. Make sure you have maven installed and deployed the Alfresco specific dependencies into your local maven repo. See the Gab's tutorial  to  [MaintainYourRepository](http://code.google.com/p/maven-alfresco-archetypes/wiki/MaintainYourRepo) or my MS Windows specific port of Gab's bootstrap script http://blogs.alfresco.com/wp/thartmann/2011/01/09/ein-alfresco-release-in-ein-lokales-maven-repository-deployen/
  1. Check out the sources for both projects.
  1. Open a commandline for both source projects and create your IDE specific configuration files i.e. for Eclipse.
```
cd PurchaseRequest
mvn eclipse:eclipse

cd PurchaseRequestShare
mvn eclipse:eclipse
```
  1. Adjust the pom.xml's properties. Both POM files point to their deployment target directory using the **alfresco.target.dir** property within the properties section.
```
    <properties>
        <alfresco.target.dir>C:/.././..</alfresco.target.dir>
```
  1. The custom deployJar default profile within the pom will trigger an ant-run copy process. The jar artifacts will automically be copied to the specified **alfresco.target.dir** directory during the execution of maven's install phase. Just deactivate the profile if you do not like that by setting the **activeByDefault** property to false. The Repository module will be copied to the webapps/alfresco/WEB-INF/lib directory. The Share artifact will be placed inside the tomcat/shared/lib directory.
```
<profiles>
        <profile>
            <id>deployJar</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
```
  1. Build and deploy the Repository artifact `mvn clean install`
  1. Build and deploy the Share artifact `mvn clean install`
  1. Restart your Alfresco instance and check the log for errors.
  1. Login to Alfresco Share and add the Purchase Request dashlet to a  Share Site Dashboard.
  1. To verify that everything is in place and works just click the link. The edit and submit the form and check if the document has been created, all values have been filled out correctly and that the workflow has been started and assigned to the approver.

