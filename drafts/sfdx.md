# SFDX

[Developer Documentation](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)

[Installing Recipes using a Scratch Org](https://github.com/trailheadapps/lwc-recipes#installing-recipes-using-a-scratch-org)

[Scratch Org Features](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs_def_file_config_values.htm)

# Authenticate
Sets the org that you login to as default and creates an alias for it  
(Set default for the create command to succeed)

```
sfdx force:auth:web:login -d -a someUserAlias
```

Auth info is written to $HOME/.sfdx  
(Note: There's also .sfdx in the project)

## Show auth info for the default org username
```
sfdx force:org:display
```
Or you can point to another username with `-u my@un.org`


# Setup

## Create a scratch org
```sh
sfdx force:org:create -s -f config/project-scratch-def.json -a someOrgAlias
```
This will display the orgId and the username if successful.

## Permissions
```
sfdx force:user:permset:assign -n recipes 
```
Note: This is for the recipes example. It comes from recipes.permissionset-meta.xml, I think 

# Coding

## Deploy Code
```
sfdx force:source:push
```

## Get changes made on the server
```
sfdx force:source:pull 
```

# Data
## Import Sample Data to the Org
```
sfdx force:data:tree:import --plan ./data/data-plan.json
```

## Export data
```
sfdx force:data:tree:export --query "SELECT Body,LastModifiedDate FROM FeedItem" -u loz@dev1.org
```

# Running

## Open Org in Browser
```sh
sfdx force:org:open
# or
sfdx force:org:open --path one/one.app
# or
sfdx force:org:open -u USER@DOMAIN
```

# Testing 

## Run APEX Tests
```
sfdx force:apex:test:run --resultformat human
```

# Administrative

## List known scratch Orgs
```
sfdx force:org:list
```

## Set default scratch org
```
sfdx force:config:list
sfdx force:config:set defaultusername=<username|alias>
```

## View how many scratch orgs you have allocated, and how many you have remaining:
```
sfdx force:limits:api:display -u <Dev Hub username or alias>
```

## Run a SOQL query against a scratch org.
```
sfdx force:data:soql:query -q "SELECT Id, name, industry, Type, NumberOfEmployees, TickerSymbol, Phone FROM Account ORDER BY createdDate ASC"
```

## Delete an existing scratch org to free up an allocation 
```
sfdx force:org:delete
```

# Packages
```
sfdx force:package:list

sfdx force:package:install --package demo-pkgA@0.1.0.1 --targetusername sub1 --instalationkey test1234 --wait 20
```

In unlocked packages and 2GPs (2nd gen), `@namespaceAccessible` classes will be accessible only by classes in the same namespace. 