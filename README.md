# rke2-rancher
Build RKE2 Cluster and Deploy Rancher

# Install Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER


# Install RKE2
curl -sfL https://get.rke2.io | sh -

Manager Node:
sudo mkdir -p /etc/rancher/rke2
cat << EOF | sudo tee /etc/rancher/rke2/config.yaml
write-kubeconfig-mode: "0644"
EOF

sudo systemctl enable rke2-server.service
sudo systemctl start rke2-server.service

Worker Nodes
** /var/lib/rancher/rke2/server/node-token
sudo mkdir -p /etc/rancher/rke2
cat << EOF | sudo tee /etc/rancher/rke2/config.yaml
server: https://35.232.55.159:9345
token: K10d0abb165302ad23e4427f3761c6cd9b444053e30d601a4c229895220a1addfd0::server:4cc208962b7ec383fcaa6c1a5c8cd452
EOF

sudo systemctl enable rke2-agent.service
sudo systemctl start rke2-agent.service

# Local Kubeconfig
cat /etc/rancher/rke2/rke2.yaml