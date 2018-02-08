```
# Start Vagrant machine
vagrant up

# After Vagrant provisioner finishes
vagrant ssh

# Clone juju repository
git clone https://github.com/juju/juju.git

# Enter repository
cd juju

# Change version and source-tag in snapcraft.yaml
sed -i '2s/version: 2.4-beta1/version: 2.1.2/' snap/snapcraft.yaml
sed -i '30s/#source-tag: juju-2.0.2/source-tag: juju-2.1.2/' snap/snapcraft.yaml

# Build snap
snapcraft

# Install snap
sudo snap install juju_2.1.2_amd64.snap --classic --dangerous

# Confirm 2.1.2 client
juju version

# Bootstrap to LXD (bootstrap series due to lp#1727355)
juju bootstrap lxd --bootstrap-series xenial

# Enable HA
juju enable-ha

# Wait for HA to deploy

# Switch to 2.3.2 snap (revert from local to snap store)
sudo snap refresh juju --revision 3230

# Confirm 2.3.2 client
juju version

# Upgrade 2.1.2 to 2.3.2
juju upgrade-juju -m controller --agent-version 2.3.2

# Wait for machines in controller model to error
juju status -m controller
```