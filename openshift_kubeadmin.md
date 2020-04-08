
# Create Simple oath htpasswd identify provider for CRC
When you start up CRC you see this message. Most things will work but some applications, such as Eclipse Che, require a configured oath source. 

This guide will explain how to setup simple oath provider.

"You are logged in as a temporary administrative user. Update the cluster OAuth configuration to allow others to log in."

## Step 1: create a password file

Command Syntax
```console
echo "Create file and add user"
htpasswd -c -B -b </path/to/users.htpasswd> <user_name> <password>
echo "Add users to file"
htpasswd -b </path/to/users.htpasswd> <user_name> <password>
```

Sample Command. Lets create a developer and an admin. Use your own passwords
```console
htpasswd -c -B -b users.htpasswd developer DemoPassword
htpasswd -b users.htpasswd admin DemoPassword
```

Verify file
```console
cat users.htpasswd 
developer:$apr1$mFhNVxo/$Ehu47oSaqXX75RaK9tq0E.
admin:$apr1$sCDKjU9T$lZsFg/j3yQ2E6KKluxt3J/
```

## Creating the HTPasswd Secret in OpenShift

To use the HTPasswd identity provider, you must define a secret that contains the HTPasswd user file.

Login as current admin
```console
oc login -u kubeadmin -p [your kubeadmin password] https://api.crc.testing:6443
```

create secret
```console
oc delete secret htpass-secret -n openshift-config

oc create secret generic htpass-secret --from-file=htpasswd=users.htpasswd -n openshift-config
```

test user login
```console
oc login -u admin -p DemoPassword https://api.crc.testing:6443
```

## Give admin user cluster admin privileges
Login as current admin
```console
oc login -u kubeadmin -p [your kubeadmin password] https://api.crc.testing:6443
oc create clusterrolebinding registry-controller --clusterrole=cluster-admin --user=admin
```

## Delete kubeadmin If that all worked
```console
oc login -u admin -p DemoPassword https://api.crc.testing:6443
oc delete secrets kubeadmin -n kube-system
```
