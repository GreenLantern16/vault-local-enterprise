## Run a Local Vault Instance (Enterprise) 


![889D658B-012A-469B-8C22-BFD069C2F270](https://user-images.githubusercontent.com/88564478/150195290-efdcaf07-8c7d-47f3-9727-d61887b2bb5c.jpeg)





**Create directory Structure (Example)**


``
mkdir /Users/<your-user-name>/vault_local
``  


``
mkdir /Users/<your-user-name>/vault_local/data
``  


**Download existing Enterprise Binaries**

Pay Attention it should look like this URL: https://releases.hashicorp.com/

![6904D405-7EA2-4438-9BCD-303359BB1D29](https://user-images.githubusercontent.com/88564478/150195272-c09a690a-7af3-4ab5-8f05-7d3267df5df5.jpeg)





![BA25EF5C-FE90-4E93-9F08-DB8FBA9562A0_4_5005_c](https://user-images.githubusercontent.com/88564478/150195296-7113cab1-76ae-424e-b421-7af531c5f2e6.jpeg)






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

#Set env vars for Vault if needed 

export VAULT_ADDR='http://127.0.0.1:8200'



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
 
#The Vault CLI Command is deprciated place licnese in path and run vault

```




``
Open a browser and go to http://127.0.0.1:8200
``







