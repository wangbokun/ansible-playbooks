### What should I change to run it?




VIP: 10.10.10.10
presto-001: 10.10.10.1
presto-002: 10.10.10.2


First, you need to spin up 2 EC2 instances and assign a ```secondary``` IP address to one of them.

Then change the following variables inside **defaults**:
```
# private IP addresses of ec2 instances
master_ip_address:
slave_ip_address:

VIP:  # instance's secondary IP address
VIP_subnet: 20 # CIDR netmask of a subnet the VIP belongs to
```
You'll also need to change variables in **var/main.yml**:
```
#如果配置了role可以不用写key，直接写上region就可以
aws_access_key:
aws_secret_key:
region:
```
But before you do this, create an IAM user with appropriate access policy. You can create a custom policy using contents of **aws_policy_example** file in this repo, then attach this policy to a new user.

Of course, don't forget to change the path to your private key in ansible.cfg:
```
private_key_file = ~/.ssh/express42
```
and change IP address of freeradius host in ```hosts``` file.

### How to run?

You can use the following command:
```
ansible-playbook site.yml
```




#Q&&A 

```
使用一个公共的域名，presto-coordinator-master 生成keytab，并且更新hosts文件.  presto-coordinator-master需要些到第二列
10.10.10.1   presto-coordinator-master.net presto-coordinator-master presto-001.net tpresto-001

```