## Installing elastic

- To install elasticseach, follow the installation process on the official elasticsearch documentation page:
https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html

- The same for Kibana at:
https://www.elastic.co/guide/en/kibana/current/install.html

To enabling the **writting rules features**, be sure to set 32 string of character in the kibana config file `kibana.yml`.
````
# X-Pack Key 
xpack.security.encryptionKey:"something_at_least_32_characters"
````

## Install Zeek

You can follow the installation process on the following page : 
https://medium.com/@cybertoolguardian/zeek-installation-in-ubuntu-60835ee3e42c

## Configure filebeat with Zeek
Following  which kind of Zeek's logs (eg: conn.log, dns.log,...) you want to visualize in kibana, you can configure **filebeat** to chip these logs to kibana.

Follow the detailed instructions on this link below to configure it:

https://www.elastic.co/blog/collecting-and-analyzing-zeek-data-with-elastic-security

