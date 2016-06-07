# data-gov-virtuoso-scripts

From https://data-gov.tw.rpi.edu/wiki/How_to_install_virtuoso_sparql_endpoint

Start-up/Shutdown Scripts

We have come up with some command line scripts on 64bit Linux (CentOS 5) to start-up/shutdown/restart the Virtuoso server instance and SPARQL endpoint in a single command.

To start the Virtuoso instance:
sudo /etc/init.d/virtuosod start

To stop the Virtuoso instance:
sudo /etc/init.d/virtuosod stop

To restart the Virtuoso instance:
sudo /etc/init.d/virtuosod restart

Please note that:
All commands require sudo privileged user accounts.
Once the Virtuoso server instance is started successfully, the SPAQL endpoint will immediately become accessible at
http://<host>:<port>/sparql

In order to start the Virtuoso instance correctly, please make sure there are no existing live Virtuoso instances running under the directory of /usr/local/virtuoso-opensource/var/lib/virtuoso/db. Otherwise, the startup command will fail due to the file locking mechanisms used by the Virtuoso implementation.

Loading Triples

We have come up with some command line utility scripts for loading triples in different formats into a named graph in the Virtuoso triple store. The scripts are located at
/opt/scripts

The formats supported are:
RDF/XML
Turtle
N-triples
N-quad

Please follow these steps to load a data file (in either of the formats above) into a named graph:
cd to /opt/scripts.
cd /opt/scripts

run the script vload, with exactly three arguments:
format: [rdf | ttl | nt | nq] corresponds to RDF/XML, Turtle, N-triples, and N-quad respectively.
data_file: path to the raw data file.
graph_uri: named graph uri into which the triples should be loaded
sudo ./vload nt /path/to/data/file/data-1554.nt http://data-gov.tw.rpi.edu/vocab/Dataset_1554

wait until the loading finishes. Depending on the size of the loaded dataset, this might take several seconds to several hours.
also see http://data-gov.tw.rpi.edu/2010/virtuoso/vload

Deleting Named Graphs

There is a utility command for deleting a specific named graph from the triple store. It is located at
/opt/scripts
It takes only one argument, the URI of the named graph to be deleted. So, to delete all the triples in the named graph <http://data-gov.tw.rpi.edu/vocab/Dataset_1554>, you can use the following command.

sudo ./vdelete http://data-gov.tw.rpi.edu/vocab/Dataset_1554
also see http://data-gov.tw.rpi.edu/2010/virtuoso/vdelete
