## PrestaShop on Dokku

This is a basic Dockerfile based dokku deploy that will setup PrestaShop
1.6.1.6.

### Installation

1. Create an app
```
dokku create myshop
```
2. Create a mariadb/mysql instance and link it to this container:
```
dokku mariadb:create myshop-database
dokku mariadb:link myshop-database myshop
```
3. Clone this repo and add the git remote of your server, making sure to replace
`my-server` with your host running Dokku
```
git clone https://github.com/benkaiser/prestashop-dokku.git
cd prestashop-dokku
git remote add dokku dokku@my-server:myshop
```
4. Deploy! (this step can take a while due to fetching dependencies)
```
git push dokku master
```
5. Your app will be available at ```myshop.my-server```. Head over there, it
will prompt you through a few steps. When it asks for database credentials, use
the ones listed when you linked the mariadb container in the `DATABASE_URL`
variable
6. It will ask you upon completing the install to delete the `install` folder
and rename the `admin` folder. To do this you will want to on the dokku host:
```
dokku enter myshop
rm -rf install
mv admin adminRANDOM
```
Where `adminRANDOM` is the new name for the admin directory that you will access
in your browser (`RANDOM` can be replaced with anything)
7. Your admin backend should now be accessible via
`myshop.my-server.com/adminRANDOM`
8. ???
9. Profit!

### Things not covered

1. Setting up outgoing mail (point the app to a SMTP server in the settings)
2. Changing the domain (see [dokku-domains](https://github.com/dokku/dokku/blob/master/docs/configuration/domains.md))
3. Enabling ssl for the domain (see [dokku-letsencrypt](https://github.com/dokku/dokku-letsencrypt))
