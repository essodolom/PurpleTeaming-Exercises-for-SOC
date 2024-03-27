# Install elastic

- To install elasticseach, follow the installation process on the official elasticsearch documentation page:
https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html

- The same for Kibana at:
https://www.elastic.co/guide/en/kibana/current/install.html

To enabling the **writting rules features**, be sure to set 32 string of character in the kibana config file `kibana.yml`.
````
# X-Pack Key 
xpack.security.encryptionKey:"something_at_least_32_characters"
````

- To install ***filebeat***, follow the steps at this links :
  https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html
  
- To install ***Winlogbeat*** follow the steps at this links:
  https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-installation-configuration.html
  
  - To configure ***sysmon*** as well, with winlogbeat, in the *`winlogbeat.yml`*, under  *`winlogbeat.event_log`*, specify the sysmon event logs that will be monitored. See this exeample below :
    
    ```
    winlogbeat.event_logs:
      - name: Microsoft-Windows-Sysmon/Operational
    ```

    


# Install Zeek

You can follow the installation process on the following page : 
https://medium.com/@cybertoolguardian/zeek-installation-in-ubuntu-60835ee3e42c

## Configure filebeat with Zeek
Following  which kind of Zeek's logs (eg: conn.log, dns.log,...) you want to visualize in kibana, you can configure ***filebeat*** to chip these logs to kibana.

Follow the detailed instructions on this link below to configure it:
https://www.elastic.co/blog/collecting-and-analyzing-zeek-data-with-elastic-security

