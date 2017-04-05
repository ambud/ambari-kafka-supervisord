# Ambari-kafka-supervisord
Ambari Kafka stack override to control Kafka via Supervisord instead of standard Ambari process control mechanisms.

The stack override is also responsible to install Supervisord and deploy the Kafka supervisord service configuration to enable Supervisord to manage Kafka process.

# Pre-requisites

1. Ambari server (>2.4) is installed, setup and stopped
2. Ambari agents are installed, configured and stopped
3. Ambari agent cache is cleared i.e. ```sudo rm -rf /var/lib/ambari-agent/cache/*```
4. Kafka is NOT installed

# Usage

1. Package the contents of the stack to a tarball ```tar czf stack.tgz metainfo.xml package```
2. SCP the ```stack.tgz``` to your Ambari server
3. Unpack the stack.tgz file using ```mkdir output; tar xvf stack.tgz -C output```
4. Now copy the contents of the folder to Ambari stacks ```sudo cp output/* /var/lib/ambari-server/resources/common-services/KAFKA/0.8.1/```
5. Start Ambari server ```sudo ambari-server start```
6. Start Ambari agents ```sudo service ambari-agent restart```
7. Wait for the agents to be discovered on Ambari
8. Deploy Kafka via Ambari and perform your standard configuration
9. Enable Supervisord autostart, on RHEL using ```sudo chkconfig supervisord on```
