apt-get update && apt-get upgrade -y

apt-get install build-essential jq python-dev python-pip python3-dev python3-pip -y

curl -fsSL https://get.docker.com | bash

wget https://golang.org/dl/go1.16.2.linux-amd64.tar.gz

rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.2.linux-amd64.tar.gz && rm -rf go1.16.2.linux-amd64.tar.gz

echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.bashrc

go version

pip install pyyaml

echo "export working_dir=\"\$(go env GOPATH)/src/k8s.io\"" >> ~/.bashrc

echo "export user=$USER" >> ~/.bashrc

mkdir -p $working_dir

cd $working_dir

git clone https://github.com/$user/kubernetes.git

cd $working_dir/kubernetes

git remote add upstream https://github.com/kubernetes/kubernetes.git

git remote set-url --push upstream no_push

git remote -v

./hack/install-etcd.sh

echo "export PATH=\"\${PATH}:\$GOPATH/src/k8s.io/kubernetes/third_party/etcd\"" >> ~/.bashrc