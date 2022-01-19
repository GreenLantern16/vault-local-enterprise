## Run a Local Vault Instance (Enterprise) 

**Create directory Structure (Example)**


``
mkdir /Users/<your-user-name>/vault_local
``  


``
mkdir /Users/<your-user-name>/vault_local/data
``  


**Download existing Enterprise Binaries**

Pay Attention it should look like this URL: https://releases.hashicorp.com/


``
click on the correct version or curl it send to your working directory
``  

You may already have Vault OSS installed; ensure you create a soft link and move the binary - for example do:


``
unzip vault-enterprise_1.9.2+ent_darwin_amd64.zip
``  


``
which vault
``

Move the OSS version and add the path for the ent; something like this

``
mv vault /usr/local/bin/vault_1.9.2_ent
``

``
ln -s /usr/local/bin/vault_1.9.2_ent /usr/local/bin/vault
``

Confirm with:

``
vault -v
``

obtain your license contact HashiCorp SE or admin URL: https://license.hashicorp.services/customers


``
mv vault.hclic /Users/<your-user-name>/vault-enterprise/vault_local/data/vault.hclic
``


``
touch vault-config.hcl
``


``
nano vault-config.hcl
``
### Configure Vault for Local Storage Backend


```
storage "file" {
  path    = "/Users/<your-user-name>/vault-enterprise/vault_local/data"
}
 
ui = true
license_path = "/Users/<your-user-name>/vault-enterprise/vault_local/data/vault.hclic"
 
listener "tcp" {
 address     = "0.0.0.0:8200"
 tls_disable = 1
}
```


### Start Vault for the First Time 



``
touch local-vault-info
``



``
nano local-vault-info
``


Add this to make your local use easier




```

#Use this command to start the Vault binary and reference the config.hcl file
sudo vault server -config vault-config.hcl
 
#Vault is now running and log outputs will show in this terminal window
#Open another terminal window to continue interacting with Vault
#Use this command to initialize Vault with a single key shard
vault operator init -key-shares=1 -key-threshold=1
 
#Copy the Unseal Key and Root Token to add to this file
#This will be required for continued use of this Vault instance in the future
Unseal Key 1: <your-unseal-key>
Initial Root Token: <your-root-token>
 
#Use this command to unseal the Vault
vault operator unseal <your-unseal-key>
 
#Use this command to log into Vault as Root
vault login <your-root-token>
 
#Use this command to license your Vault enterprise binary
vault write /sys/license text="<your-license-key"
 
#Use this command to verify the license was applied
vault read /sys/license
```




``
Open a browser and go to http://127.0.0.1:8200
``







