### You Will Have all these features setup if you run this Terraform 


![5AACAAB4-50FF-4646-9A81-F8A46A78CDBE](https://user-images.githubusercontent.com/88564478/150194756-4c4037a0-4325-40b2-8a33-1f51ed52c505.jpeg)





Set the client token in the VAULT_TOKEN environment variable. If not using the root token, be sure that this token has permissions to create policies, enable secrets engines, and enable auth methods.

``
export VAULT_TOKEN="<token>"
``


Set the target Vault server address in the VAULT_ADDR environment variable if it's not done so already.


``
export VAULT_ADDR="http://127.0.0.1:8200"
``


### This will give you a full demo of Namespaces, Trasit Features, etc.




``
terraform init
``


``
terraform apply
``
