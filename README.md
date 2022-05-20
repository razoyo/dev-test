# Razoyo developer test

This excercise will test your ability to deploy open source software and make modifications to a custom module.

This codebase has been verified to work on a Ubuntu Server 20.04 LTS virtual machine running on VirtualBox. You may deploy the code to any environment you would like, but this document was written for Ubuntu 20.04.

## Install Environment

The Magento 2 stack requirements include PHP 7.4, MySQL, and Elasticsearch. Most of these packages can be installed directly from the Ubuntu apt repositories. Installing the correct version of Elasticsearch will require adding the Elastic apt repository.

### Resources
* [Obtaining Magento 2 composer keys](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html)
* [Magento 2 system requirements](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html)
* [Installing Elasticsearch 7.x](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html)

## Install Magento

The installation process will require the use of the _bin/magento_ command.

```
php bin/magento setup:install
# you will need to provide the correct options (i.e. MySQL credentials)

# Run the Magento build commands
php bin/magento deploy:mode:set developer
php bin/magento setup:upgrade
php bin/magento setup:di:compile
```

Once Magento 2 is installed, you should be able to see a blank Luma theme home page.

![Luma theme homepage](http://assets.razoyo.com/dev-test/after-installation.png)

For this excercise, it will be helpful to deploy the Magento 2 sample data. This will require 2 commands.

```
php bin/magento sampledata:deploy
php bin/magento setup:upgrade
```

After the sample data is installed, the home page should have more content.

![Sample data homepage](http://assets.razoyo.com/dev-test/after-sample-data.png)

I would also reccomend disabling the 2 factor authentication so it is easier to login to the admin panel.

```
php bin/magento module:disable Magento_TwoFactorAuth
php bin/magento cache:flush
php bin/magento setup:upgrade
php bin/magento setup:di:compile
```

## Animal profile module

This Magento codebase has a custom module installed called *Razoyo_AnimalProfile* that allows a customer to have an animal profile photo associated with their customer account.

You can see this photo in the My Account dashboard by following these steps.

#### Step 1 - Login to the admin panel with the credentials you created during Magento installation.

#### Step 2 - Go to the customer grid. Since we deployed the sample data, there should be at least 1 customer there.
![Customer grid](http://assets.razoyo.com/dev-test/customer-grid.png)

#### Step 3 - Enable remote shopping assistance for the customer. This will allow you to login as them.
![Customer remote shopping](http://assets.razoyo.com/dev-test/customer-remote-shopping.png)

#### Step 4 - Login as the customer.
![Login as customer](http://assets.razoyo.com/dev-test/login-as-customer.png)

This should open a new window and take you to the customer account dashboard, where you will see the link to the "Animal Profile" page.
![Customer dashboard](http://assets.razoyo.com/dev-test/customer-dashboard.png)

#### Step 5 - View the animal profile photo
Click on _Animal Profile_ to see the current profile photo for the customer.
![Animal profile](http://assets.razoyo.com/dev-test/animal-profile.png)

## The test requirements

Currently, the profile photo is always a cat, and there is no way to change it. We would like to give the user the ability to choose from several animal photos.

Update the *Razoyo_AnimalProfile* module so that there is a _select_ dropdown that allows you to choose between the following animals as your profile:
* Cat
* Dog
* Llama
* Anteater

When you select a different animal, the profile photo should change. The selection does **not** need save permanently. It is OK if refreshing the page reverts back to the cat photo.

### Extra Credit
Implement the ability to save the animal selection so that refreshing the page keeps your animal selection.

### Submit your work
When you have completed the feature, send an email to: assessments@razoyo.com

The email needs to contain a link to your own git repository branch with the code submission.

Please do *not* submit a pull request.
