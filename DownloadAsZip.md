# Introduction #

The "download as zip" module contains a toolbar action that triggers the download of multiple files within a folder at once, by compressing them into a zip and streaming down the zip file.
The process of compression and the streamed download is handled by a java backed webscript in the repository webscript tier.

# Details #

The "download as zip" module consists of a toolbar action and a java backed webscript compress and to stream the zip.
The screenshot shows how to download multiple selected files within the document library by just selecting them and clicking the toolbar action.

http://alfresco-application-samples.googlecode.com/issues/attachment?aid=30000000&name=downloadaszip-menu_guided.PNG&token=772e85eec175706b1dd63838fa42a54e&inline=1


http://alfresco-application-samples.googlecode.com/issues/attachment?aid=30000001&name=downloadaszip-dialog.PNG&token=2678bdc3af99ee71db713d4c2e75d90f&inline=1

# Installation #

The module consists of two components:
**a Share part that contains the UI** a repository part that contains a java backed webscript.
The Repo part is responsible for the whole zip packaging and streaming work.
The module is intended to be deployed as a JAR file.
The build script contains the whole amp packaging targets, too. But to be honest I never tested it with this module.

### Checkout and build ###

Checkout the project using svn co http://code.google.com/p/alfresco-application-samples/source/browse/trunk/DownloadAsZip

To build the JAR file, run the following command from the base project
directory.
```
ant clean dist-jar
```

### One fits all ###
The JAR file contains the Share extension as well as the repo extension So just drop a copy of the JAR into each WEB-INF/lib folder (alfresco/WEB-INF/lib and the share/WEB-INF/lib directories) and restart both.
Avoid to deploy into shared/lib as long as Share and the Repository run within the same instance as the may occur classloading issues when the repository tries to load the JAR.
