# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
sudo yum -y install ntp ntpdate ntp-doc yum-plugin-priorities
sudo ntpdate ntp.lip6.fr
sudo iptables -F
sudo setenforce 0
sudo sed -i s/=enforcing/=permissive/ /etc/sysconfig/selinux
sudo systemctl disable firewalld
sudo systemctl stop firewalld
if [ `hostname` == "ceph1" ]
then
  echo Installing ceph-deploy
  cat <<EOF | sudo tee /etc/yum.repos.d/ceph-deploy.repo
[ceph-noarch]
name=Ceph noarch packages
baseurl=http://ceph.com/rpm-hammer/el7/noarch
enabled=1
gpgcheck=1
type=rpm-md
gpgkey=https://ceph.com/git/?p=ceph.git;a=blob_plain;f=keys/release.asc
EOF
  # sudo yum -y update
  sudo yum -y install ceph-deploy
  cat > /home/vagrant/.ssh/id_rsa <<EOF
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzI
w+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoP
kcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2
hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NO
Td0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcW
yLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQIBIwKCAQEA4iqWPJXtzZA68mKd
ELs4jJsdyky+ewdZeNds5tjcnHU5zUYE25K+ffJED9qUWICcLZDc81TGWjHyAqD1
Bw7XpgUwFgeUJwUlzQurAv+/ySnxiwuaGJfhFM1CaQHzfXphgVml+fZUvnJUTvzf
TK2Lg6EdbUE9TarUlBf/xPfuEhMSlIE5keb/Zz3/LUlRg8yDqz5w+QWVJ4utnKnK
iqwZN0mwpwU7YSyJhlT4YV1F3n4YjLswM5wJs2oqm0jssQu/BT0tyEXNDYBLEF4A
sClaWuSJ2kjq7KhrrYXzagqhnSei9ODYFShJu8UWVec3Ihb5ZXlzO6vdNQ1J9Xsf
4m+2ywKBgQD6qFxx/Rv9CNN96l/4rb14HKirC2o/orApiHmHDsURs5rUKDx0f9iP
cXN7S1uePXuJRK/5hsubaOCx3Owd2u9gD6Oq0CsMkE4CUSiJcYrMANtx54cGH7Rk
EjFZxK8xAv1ldELEyxrFqkbE4BKd8QOt414qjvTGyAK+OLD3M2QdCQKBgQDtx8pN
CAxR7yhHbIWT1AH66+XWN8bXq7l3RO/ukeaci98JfkbkxURZhtxV/HHuvUhnPLdX
3TwygPBYZFNo4pzVEhzWoTtnEtrFueKxyc3+LjZpuo+mBlQ6ORtfgkr9gBVphXZG
YEzkCD3lVdl8L4cw9BVpKrJCs1c5taGjDgdInQKBgHm/fVvv96bJxc9x1tffXAcj
3OVdUN0UgXNCSaf/3A/phbeBQe9xS+3mpc4r6qvx+iy69mNBeNZ0xOitIjpjBo2+
dBEjSBwLk5q5tJqHmy/jKMJL4n9ROlx93XS+njxgibTvU6Fp9w+NOFD/HvxB3Tcz
6+jJF85D5BNAG3DBMKBjAoGBAOAxZvgsKN+JuENXsST7F89Tck2iTcQIT8g5rwWC
P9Vt74yboe2kDT531w8+egz7nAmRBKNM751U/95P9t88EDacDI/Z2OwnuFQHCPDF
llYOUI+SpLJ6/vURRbHSnnn8a/XG+nzedGH5JGqEJNQsz+xT2axM0/W/CRknmGaJ
kda/AoGANWrLCz708y7VYgAtW2Uf1DPOIYMdvo6fxIB5i9ZfISgcJ/bbCUkFrhoH
+vq/5CIWxCPp0f85R4qxxQ5ihxJ0YDQT9Jpx4TMss4PSavPaBH3RXow5Ohe+bYoQ
NE5OgEXk2wVfZczCZpigBKbKZHNYcelXtTt/nP3rsCuGcM4h53s=
-----END RSA PRIVATE KEY-----
EOF
  chmod 600 /home/vagrant/.ssh/id_rsa
  sudo chown vagrant:vagrant /home/vagrant/.ssh/id_rsa
  cat > /home/vagrant/.ssh/id_rsa.pub <<EOF
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ== vagrant insecure public key
EOF
  sudo chown vagrant:vagrant /home/vagrant/.ssh/id_rsa.pub
  chmod 644 /home/vagrant/.ssh/id_rsa.pub
  cat > /home/vagrant/.ssh/config <<EOF
Host *
   StrictHostKeyChecking no
   UserKnownHostsFile=/dev/null
EOF
  sudo chown vagrant:vagrant /home/vagrant/.ssh/config
  chmod 600 /home/vagrant/.ssh/config
  ceph-deploy new ceph1 ceph2 ceph3
  ceph-deploy install ceph1 ceph2 ceph3
  ceph-deploy mon create ceph1 ceph2 ceph3
  ceph-deploy gatherkeys ceph1
  ceph-deploy disk zap ceph1:/dev/vda
  ceph-deploy disk zap ceph1:/dev/vdb
  ceph-deploy disk zap ceph2:/dev/vda
  ceph-deploy disk zap ceph2:/dev/vdb
  ceph-deploy disk zap ceph3:/dev/vda
  ceph-deploy disk zap ceph3:/dev/vdb
  ceph-deploy disk prepare ceph1:/dev/vda:/dev/vdb
  ceph-deploy disk prepare ceph2:/dev/vda:/dev/vdb
  ceph-deploy disk prepare ceph3:/dev/vda:/dev/vdb
  ceph-deploy disk activate ceph1:/dev/vda1
  ceph-deploy disk activate ceph2:/dev/vda1
  ceph-deploy disk activate ceph3:/dev/vda1
  ceph-deploy mds create ceph1 ceph2 ceph3

  sudo ceph-authtool --create-keyring /etc/ceph/ceph.client.radosgw.keyring
  sudo chmod +r /etc/ceph/ceph.client.radosgw.keyring
  sudo ceph-authtool /etc/ceph/ceph.client.radosgw.keyring -n client.radosgw.gateway --gen-key
  sudo ceph-authtool -n client.radosgw.gateway --cap osd 'allow rwx' --cap mon 'allow rwx' /etc/ceph/ceph.client.radosgw.keyring
  sudo ceph -k /etc/ceph/ceph.client.admin.keyring auth add client.radosgw.gateway -i /etc/ceph/ceph.client.radosgw.keyring

  sudo bash -c 'echo "[client.radosgw.gateway]" >> /etc/ceph/ceph.conf'
  sudo bash -c 'echo "host = ceph1" >> /etc/ceph/ceph.conf'
  sudo bash -c 'echo "keyring = /etc/ceph/ceph.client.radosgw.keyring" >> /etc/ceph/ceph.conf'
  sudo bash -c 'echo "rgw socket path = /var/run/ceph/ceph.radosgw.gateway.fastcgi.sock" >> /etc/ceph/ceph.conf'
  sudo bash -c 'echo "log file = /var/log/radosgw/client.radosgw.gateway.log" >> /etc/ceph/ceph.conf'
  sudo bash -c 'echo "rgw print continue = false" >> /etc/ceph/ceph.conf'
  sudo yum -y install httpd
  sudo mkdir -p /var/lib/ceph/radosgw/ceph-radosgw.gateway
  sudo systemctl start ceph-radosgw
  sudo chown apache:apache /var/run/ceph

  cat <<EOF | sudo tee /etc/httpd/conf.d/rgw.conf
<VirtualHost *:80>
  ServerName ceph1
  DocumentRoot /var/www/html
  ErrorLog /var/log/httpd/rgw_error.log
  CustomLog /var/log/httpd/rgw_access.log combined
  # LogLevel debug
  RewriteEngine On
  RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization},L]
  SetEnv proxy-nokeepalive 1
  ProxyPass / unix:///var/run/ceph/ceph.radosgw.gateway.fastcgi.sock|fcgi://localhost:9000/
</VirtualHost>
EOF

  sudo systemctl start httpd

  sudo radosgw-admin user create --uid="testuser" --display-name="Test User"
  sudo radosgw-admin subuser create --uid=testuser --subuser=testuser:swift --access=full
  sudo radosgw-admin key create --subuser=testuser:swift --key-type=swift --gen-secret &> secret

  sudo yum -y install jq
  echo "export ST_AUTH=http://ceph1/auth/1.0" > swiftrc
  echo "export ST_USER=testuser:swift" >> swiftrc
  echo "export ST_KEY=`cat secret | jq .swift_keys[0].secret_key | cut -d '"' -f 2`" >> /vagrant/swiftrc
fi
SCRIPT

Vagrant.configure(2) do |config|
  # config.vm.box = "webhippie/centos-7"
  config.vm.box = "centos7"

  # SSH configuration
  config.ssh.forward_agent = true
  config.ssh.insert_key = false

  # vagrant-hostmanager configuration
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  # Ceph provision
  config.vm.provision "shell", inline: $script, privileged: false

  # Add one disk for data and one disk for journal
  config.vm.provider "libvirt" do |libvirt|
    libvirt.storage :file, :size => '20G'
    libvirt.storage :file, :size => '10G'
    libvirt.memory = 1024
  end

  config.vm.define "ceph1" do |ceph1|
    ceph1.vm.hostname = "ceph1"
  end

  config.vm.define "ceph2" do |ceph2|
    ceph2.vm.hostname = "ceph2"
  end

  config.vm.define "ceph3" do |ceph3|
    ceph3.vm.hostname = "ceph3"
  end
end
