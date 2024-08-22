# Mautic LDAP Single Sign-On Authentication Plugin

This Plugin enables LDAP authentication for Mautic. Even though Mautic offers SAML authentication, the main objective is to offer an alternative to those who do not want to setup larger SSO in their company just for mautic :smiley:

## Installation via composer (preferred)
Execute `composer require leuchtfeuer/mautic-ldapauth-bundle` in the main directory of the mautic installation.

## Installation via .zip
1. Download the [master.zip](https://github.com/Leuchtfeuer/Mautic-LdapAuth-Bundle/archive/master.zip), extract it into the `plugins/` directory and rename the new directory to `MauticLdapAuthBundle`.
2. Install `symfony/ldap` requirements with composer: `composer require symfony/ldap:~2.8`
3. Clear the cache via console command `php app/console cache:clear --env=prod`  *OR* manually delete the `app/cache/prod` directory.

## Configuration
Navigate to the Plugins page and click "Install/Upgrade Plugins". You should now see a "LDAP Auth" plugin.

-   ![LDAP Auth Plugin](docs/mautic_ldap_plugins_01.png)
-   ![LDAP Auth Plugin - Published](docs/mautic_ldap_plugins_02.png)
-   ![LDAP Auth Plugin - Features](docs/mautic_ldap_plugins_03.png)

Make sure to have the desired settings, specifically "Role for created user".

After activating the plugin, you can now go to "Configuration > LDAP Settings" to edit the parameters:

![LDAP Settings](docs/mautic_ldap_settings_02.png)

You can also edit manually your parameters in `local.php` (adapt to your LDAP configuration):
```php
    //'parameters' => array(
    // ...
        'ldap_auth_host' => 'ldap.mysupercompany.com',
        'ldap_auth_port' => 389,
        'ldap_auth_version' => 3,
        'ldap_auth_ssl' => false,
        'ldap_auth_starttls' => true,
        'ldap_auth_base_dn' => 'ou=People,dc=ldap,dc=mysupercompany,dc=com',
        'ldap_auth_user_query' => '(objectclass=inetOrgPerson)',
        'ldap_auth_username_attribute' => 'uid',
        'ldap_auth_email_attribute' => 'mail',
        'ldap_auth_firstname_attribute' => 'givenname',
        'ldap_auth_lastname_attribute' => 'sn',
        'ldap_auth_fullname_attribute' => 'displayname',
        'ldap_auth_isactivedirectory' => false,
    // ...
```

A sample configuration for Active Directory is 
```php
    //'parameters' => array(
    // ...
        'ldap_auth_host' => 'ad.mysupercompany.com',
        'ldap_auth_port' => 389,
        'ldap_auth_version' => 3,
        'ldap_auth_ssl' => false,
        'ldap_auth_starttls' => false,
        'ldap_auth_base_dn' => 'cn=Users,dc=ad,dc=mysupercompany,dc=com',
        'ldap_auth_user_query' => '(objectclass=user)(memberof=marketing)',     // careful this can be case sensitive!
        'ldap_auth_username_attribute' => 'samaccountname',                     // this is case sensitive!
        'ldap_auth_email_attribute' => 'mail',
        'ldap_auth_firstname_attribute' => 'givenName',
        'ldap_auth_lastname_attribute' => 'sn',
        'ldap_auth_fullname_attribute' => 'displayName',
        'ldap_auth_isactivedirectory' => true,
        'ldap_auth_activedirectory_domain' => 'ad.mysupercompany.com',
    // ...
```

Once the parameters are set, open a new browser and check connection through LDAP. **Do not log out until LDAP configuration is valid!**

## Known limitations

* Active Directory support currently abandoned
* only default group assignment (not based on LDAP attributes)
* LDAP attributes in the configuration not matching the actual data (e.g. misspelled, like givenname instead of givenName) prevent the plugin from working

## Contributing

Ideas and suggestions are welcome. Feel free to create an issue or PR on Github using our [CONTRIBUTING](CONTRIBUTING.md) guidelines.

## License

See [LICENSE](LICENSE) file.

## Author(s)
Original authors: [Monogramm](https://github.com/Monogramm)

Authors and maintainers of this fork: * [Leuchtfeuer Digital Marketing](https://Leuchtfeuer.com)

## Awesome contributor(s)

* [terdinatore](https://github.com/terdinatore)
