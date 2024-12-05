# Requirements
- NodeJS 20

# Installation

First, clone the repository

``` bash
git clone https://github.com/Twit-Snap/twitsnap-backoffice.git
```
Then, if you want to install the requirements to continue with the development run:

``` bash
npm install
```

# Run it

### Run in development

```bash
npm run dev
```

### Run in production

#### Build

```bash
npm run build
```

#### Run

```bash
npm run start
```

### Run linter

```bash
npm run lint
```


# Environment variables

- **NEXT_PUBLIC_TWIT_SERVER_URL:** Environment variable for the twit server url
- **NEXT_PUBLIC_USER_SERVER_URL:** Environment variable for the user server url
- **NEXT_PUBLIC_METRICS_SERVER_URL:** Environment variable for the metrics server url




# User Guide 

This is the backoffice web for the Twitsnap project. It is a project that allows an administrator to manage the users and twits and collect metrics of the Twitsnap project.

As administrator, in the main page you will see the following options:

- **Administrator Sing Up:** 
- **Users**
- **Twits** 
- **Metrics** 

## Administrator Sing Up

In this section you can register a new administrator. You must enter the following information:

- **Name:** Name of the administrator
- **Email:** Email of the administrator
- **Password:** Password of the administrator
- **Confirm Password:** Confirm the password of the administrator
- **Register:** Button to register the administrator

## Users

In this section you can see the list of users of the Twitsnap project. You can see the following information:

- **Name:** Name of the user
- **Username:** Username of the user
- **Email:** Email of the user
- **Creation date:** Date of creation of the user
- **Private:** If the user is private or not
- **Block:** If the user is blocked or not and the option to block or unblock the user

Clicking on the user you can see the complete information of the user.

## Twits

In this section you can see the list of twits of the Twitsnap project. You can see the following information:

- **Id:** Id of the twit
- **Username:** Username of the user who made the twit
- **Creation date:** Date of creation of the twit
- **Content:** Content of the twit
- **Block:** If the twit is blocked or not and the option to block or unblock the twit
- 