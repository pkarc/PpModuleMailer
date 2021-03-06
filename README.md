PpModuleMailer
==============

Introduction
------------

PpModuleMailer is a simple ZF2 module that allows you to create and send mail 
queue with sql database.

Installation
------------

### Main Setup

#### With composer

1. Add this project in your composer.json:

    ```json
    "require": {
        "cobyl/PpModuleMailer": "dev-master"
    }
    ```

2. Now tell composer to download __PpModuleMailer__ by running the command:

    ```bash
    $ php composer.phar update
    ```

#### Post installation

1. Enabling it in your `application.config.php`file.

    ```php
    <?php
    return array(
        'modules' => array(
            // ...
            'PpModuleMailer',
        ),
        // ...
    );
    ```

2. Add table to database.

Please check sql/PpModuleMailer.mysql.sql. This module needs database with 
enabled transactions. 

# How to use _PpModuleMailer_

1. Adding mail to queue "registration" from controller:

    ```php
    <?php    
    $mail = new \Zend\Mail\Message();
    $mail->addTo('to@domain.com');
    $mail->addFrom('from@domain.com');
    $mail->setSubject('Subject');
    $mail->setBody('Body');
    $this->getServiceLocator()->get('PpModuleMailer')->add('registration',$mail);
    
    ```

2. or

    ```php
    <?php
    $this->getServiceLocator()
        ->get('PpModuleMailer')
        ->addMail('registration','to@d.com','Subject','Body','from@d.com');
        
    ```

3. Sending queue "registration" from console:

    ```bash
    $ php public/index.php mailer process registration
    
    ```

# Configuration

The default configuration is setup to use the system SMTP configuration.
For other ways check module.config.php

That's it!
==========

