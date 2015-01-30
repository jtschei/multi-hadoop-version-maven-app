# multi-hadoop-version-maven-app
Example maven setup showing how one application can support Hadoop1 and Hadoop2

The project includes a parent folder (multi-hadoop-version-maven-app) and three modules.

The module app-core would be where the bulk of your application would reside. Within this module you could safely perform any Hadoop API calls that exist in Hadoop1 and Hadoop2 and are not deprecated. To make an API call that is unique to a particular Hadoop version you need to create the necessary method in the two other modules. 

Accross the two app-util-hadoop1 and app-util-hadoop2 modules you will duplicate public class-method-signature that app-core will invoke. These class-methods would mask the details of the underlying Hadoop-version-specific-API calls. For this to work, the method signatures need to be the superset of necessary parameters. In app-util-hadoop1, the particular methods would invoke the Hadoop1 API methods. In app-util-hadoop2, the particular methods would invoke the Hadoop2 API methods. Both methods would return an object of the same type.

An example where you could use this would be creating a SequenceFile Writer. The API is different between Hadoop1 and Hadoop2. If you wish to avoid using deprecated methods you need a mechanism like we described above.
