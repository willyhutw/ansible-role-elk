# Ansible ELK

This is a Ansible role to install ELK Stack (Support Ubuntu14/16, CentOS7)

## Requirements

Ansible 2.x

## Role Variables

|Variable|Default Value|Description|
|---|---|---|
```es_cluster_name```|es_cluster|elasticsearch cluster name.
```number_of_shards```|1|depends on how many of your cluster node.
```number_of_replicas```|0|depends on how many of your cluster node.
```es_api_nic```|eth0/all|the nic of api listen address. if enter 'all', listen 0.0.0.0
```es_api_port```|9200|the api listen port.
```es_transport_nic```|eth0|the nic of transport listen address.
```es_transport_port```|9300|the transport listen port.
```minimum_master_nodes```|1|depends on how many of your cluster node.
```elasticsearch_address```|['127.0.0.1','127.0.1.1']|you must replace this value, enter the listen address of each elasticsear node. or pass to ansible-playbook as extra variable: {'elasticsearch_address':['10.89.155.78','10.89.155.79']}.
```curator_venv_path```|/home/curator_env|virtualenv path for curator.
```curator_log_path```|/home/curator_env/curator.log|log path for curator.
```curator_index_keep_day```|3|elasticsearch index keep days.
```curator_packages```|['click==6.7','elasticsearch==2.4.1', 'PyYAML==3.12', 'voluptuous==0.9.3', 'elasticsearch-curator==4.2.5']|package lists for curator.
```kibana_listen_nic```|eth0/all|the nic of kibana listen address. if enter 'all', listen 0.0.0.0
```kibana_listen_port```|5601|the kibana listen port.

## Role Tags

available tags of this role:
 - elasticsearch
 - logstash
 - kibana

## Example
```
### create a requirements.yml
- src: git+https://github.com/willyhutw/ansible-role-elk.git
  name: elk

### create a playbook.yml
- hosts: all
  become: yes
  roles:
    - roles/elk

### install this role
ansible-galaxy install -r requirements.yml -p ./roles

### run it!
ansible-playbook -i '192.168.33.101,' playbook.yml \
-e "ansible_ssh_user=willyhu ansible_ssh_pass=secret ansible_become_pass=secret" \
-e "es_api_nic=all es_transport_nic=enp0s3 kibana_listen_nic=all" \
-e "{'elasticsearch_address':['192.168.33.101']}" \

### or you can do partial-deploy with specific tags
ansible-playbook -i '192.168.33.101,' playbook.yml \
-e "ansible_ssh_user=willyhu ansible_ssh_pass=secret ansible_become_pass=secret" \
-e "es_api_nic=all es_transport_nic=enp0s3 kibana_listen_nic=all" \
-e "{'elasticsearch_address':['192.168.33.101']}" \
--tags elasticsearch kibana
```

## License

MIT / BSD

## Author Information

willyhu.tw@gmail.com
