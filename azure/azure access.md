# Preparing Ansible for Azure

Begin by creating a local credentials file to provide credentials to Ansible. For security reasons, credential files should only be used in development environments. Once you've successfully connected to the host virtual machine, create and open a file named credentials:

`mkdir ~/.azure`

`vim ~/.azure/credentials`

Insert the following lines into the file. Replace the placeholders with the service principal values.

```
[default]
subscription_id=<your-subscription_id>
client_id=<security-principal-appid>
secret=<security-principal-password>
tenant=<security-principal-tenant>
```

Save and close the file.

Now actually FINDING these values is the hard part. Here are the steps required to find each:

**Get Subscription ID**
- Login into your azure account.
- Select Subscriptions in the left sidebar.
- Select whichever subscription is needed.
- Click on overview.
- Copy the Subscription ID.

**Get Tenant ID**
- Login into your azure account.
- Select azure active directory in the left sidebar.
- Click properties.
- Copy the directory ID.

**Get Client ID**
- Login into your azure account.
- Select azure active directory in the left sidebar.
- Click Enterprise applications.
- Click All applications.
- Select the application which you have created.
- Click Properties.
- Copy the Application ID .

**Get Client secret**
- Login into your azure account.
- Select azure active directory in the left sidebar.
- Click App registrations.
- Select the application which you have created.
- Click on All settings.
- Click on Keys.
- Type Key description and select the Duration.
- Click save.
- Copy and store the key value. You won't be able to retrieve it after you leave this page.

Next you'll need to install the necessary Azure requirements via pip:

`wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt`

`python3 -m pip install -r requirements-azure.txt`
