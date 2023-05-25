to Create a new firewall to rule to allow a tcp port
```
az network nsg rule create --resource-group linux --nsg-name -nsg --name test --priority 100 --access allow --protocol tcp --direction Inbound --destination-port-range 62 --protocol tcp 
```