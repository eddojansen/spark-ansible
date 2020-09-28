# spark-ansible

Automated installation and configuration of a spark cluster.

# Prerequisites:
* Update all nodes with 'sudo apt update'
* Setup password less ssh on all nodes in the cluster
* Setup password less sudo on all nodes in the cluster 

## Step1: Update the inventory file where:
* The entry under [master] is where you put the hostname or IP of the spark master
* The entries under [slaves] are the nodes that are used as spark slaves/workers (The master can also be a slave, so could be under both entries) 

## Step2: Install ansible on the master node (apt/yum install -y ansible)

## Step3: Update the vars/spark.yaml file where:
* CONFIG: Is a shared storage location accesible by all nodes (NFS or Quobyte, etc)
* SPARK_DOWNLOAD_URL: Is the download url of the spark version you want to install (for example: https://archive.apache.org/dist/spark/spark-3.0.0/spark-3.0.0-bin-hadoop3.2.tgz)
* SPARK_MASTER: Is the IP address of the Spark master node
* WORKER_OPTS: Is where you can put additional startup options for the worker nodes, when not used leave the entry WORKER_OPTS: ""

## Step4: Run the playbook from the master node and within the spark-ansible directory:
* ansible-playbook -i inventory install-spark.yaml (use -vvvvvv at the end for more verbosity)

## Step5: Verify successful installation by checking http://yoursparkmasterip:8080 (you should see the master and slaves)

## Step6: Optionally clean and remove the spark installation by running:
* ansible-playbook -i inventory cleanup-spark.yaml 
