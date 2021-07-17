# Simulator-eNB-and-UE-using-docker
# Installation:
Install python-minimal:
sudo apt update && apt -y install python-minimal
Install Ansible:
sudo apt -y install ansible
Run the following Ansible playbook (password for sudo is required):
IN eNB host machine:
ansible-playbook -K docker_eNB.yml
In UE host machine:
ansible-playbook -K docker_UE.yml
# Test:
Access the eNB container:
sudo docker exec -ti enb bash
Access the UE container:
sudo docker exec -ti ue bash
In the eNB host machine, start the eNB software:
cd /root/enb/cmake_targets/ran_build/build && sudo -E ./lte-softmodem -O /root/enb/ci-scripts/conf_files/rcc.band7.tm1.nfapi.conf --noS1 > enb.log 2>&1&
In the UE host machine, start the UE software:
cd /root/ue/cmake_targets/ran_build/build && ./lte-uesoftmodem -O /root/ue/ci-scripts/conf_files/ue.nfapi.conf --L2-emul 3 --num-ues 1 --nums_ue_thread 1 --nokrnmod 1 --noS1 > ue.log 2>&1&
# test ping:
Ping UE to eNB:
ping -I oaitun_ue1 10.0.1.1
Ping eNB to UE:
ping -I oaitun_enb1 10.0.1.2
