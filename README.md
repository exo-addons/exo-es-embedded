# elasticsearch embedded add-on

This add-on embedded an ElasticSearch in eXo Platform Server.

Only localhost node can access the cluster and only localhost request to the node are accepted by default.

## Installing

1. Install ElasticSearch ingest-attachment plugin maven pom
- This step is workaround solution to fix the missing dependency issue of ingest-attachment maven POM. Follow steps to install in your local repository
- Download plugin jar from https://repository.exoplatform.org/content/groups/public/org/elasticsearch/plugin/ingest-attachment/5.3.2/ingest-attachment-5.3.2.jar
- POM file for the plugin is is the root project directory. Lets install by mvn command:
```
$ mvn install:install-file -Dfile=ingest-attachment-5.3.2.jar -DpomFile=ingest-attachment-5.3.2.pom
```

1. Build the add-on with Maven
```
$ mvn clean package
```
2. Copy ```exo-es-embedded/packaging/target/exo-es-embedded-packaging-2.0.x-SNAPSHOT.zip``` to ```$PLATFORM_HOME/addons```
3. Add the following entry in $PLATFORM_HOME/addons/local.json:
```
[
 {
 "id": "exo-es-embedded",
 "version": "2.0.x-SNAPSHOT",
 "name": "elasticsearch embedded Add-on",
 "description": "The elasticsearch embedded Add-on",
 "downloadUrl": "file://./exo-es-embedded-packaging-2.0.x-SNAPSHOT.zip",
 "vendor": "eXo platform",
 "license": "LGPLv3",
 "supportedDistributions": ["community","enterprise"],
 "supportedApplicationServers": ["tomcat","jboss"]
 }
]
```
4. Install the addon:
```
$ ./addon install exo-es-embedded --snapshots
```
5. Start PLF

## Testing

After starting eXo Platform you can test as follow:

```
$ curl -v localhost:9200
$ curl -XPUT 'http://localhost:9200/blog/user/tclement' -d '{ "name" : "Thibault Clement" }'
$ curl -v localhost:9200/blog
```
