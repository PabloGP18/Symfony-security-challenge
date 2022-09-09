# Symfony security/authentication challenge

## The project
We got this assignment as an extra because it will help us understand better how symfony works, and it's also used a lot in a real life scenario.

## The security bundle
I first started requiring the security bundle for Symfony:

`composer require symfony/security-bundle`

The SecurityBundle, provides all authentication and authorization features needed to secure your application.

## The user

After requiring the securityBundle, I made an entity user. Permissions in Symfony are always linked to a user object. You need this class if you want to secure (parts of) your application.

The way to generate the User class:

`php bin/console make:user`

After this command, you will have to answer several questions in order to configure the User class.

## Making a database and a connection with the application

When you're finished creating your User class, the terminal will ask you to migrate your class to a database, but first you need one to do this.

I made a database and a schema in datagrip.

After that I needed to  uncomment the line below in the .env file:

`DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=8&charset=utf8mb4"`

Like you can see in the example above, I used MYSQL for this application. To make the connection you will need to adapt some things.

- app: = username
- ChangeMe = password
- app? = database name
- serverVersion = version of your database technology

Now you can check the connection by migrating the User class with this 2 commands:

- `php bin/console make:migration`
- `php bin/console doctrine:migrations:migrate`

When this is successful, you will see in your database your user table.

## Hashing passwords

I made sure that the User class implements the PasswordAuthenticatedUserInterface.

`class User implements UserInterface, PasswordAuthenticatedUserInterface`

You can also hash a password manually by running:

`php bin/console security:hash-password`

## Registration 

Before login, you first want to register.

In Symfony it's possible to make a registration form:

`php bin/console make:registration-form`

## Login logic

After completing the registration part, a user should be able to log in. 
Symfony has a command that allows us to create the login logic:

`symfony console make:auth`

After this you need to answer a couple of questions how you want to configure the logic for the login. 

## Admin and Admin page

I registered an admin account, and I assigned manually the ROLE_ADMIN in the backend only to the user admin.
The rest of tu users will be by default ROLE_USER.

Then I gave the admin permission to access the admin page.
This I did by uncommenting the following line in the security.yaml:

`{ path: ^/admin, roles: ROLE_ADMIN }`

After all this I still had to make the admin page. With some research I found out something that is called easyAdmin.

I required the easyAdmin bundle: 

`composer req admin`

The good thing of the easyAdminBundle is that you can create dashboards for the admin page.
I created a dashboardcontroller to grant access to the admin and also to render the admin page.
Afther this I created a dasboard (userCrudController) for all the users where the admin can read, edit and delete the users:

`symfony console make:admin:crud`


## Conclusion

I made a basic (raw) application where a user can register, login, navigate and also added an admin with an admin page/dashboard.
It took me some work to get to the point where this was working properly, but I have to admit how powerful and nice Symfony really is.....
Symfony, I hope we meet again baby :).
Peace out!







