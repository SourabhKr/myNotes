# Important Terminology

#### Authentication

Authentication is the process by which your identity is confirmed through the use of some kind of credential.
Authentication is about proving that you are who you say you are.

#### Authorization

Authorization is the process of determining whether the principal or application attempting to access a resource has
been authorized for that level of access.

#### Credentials

For authentication, credentials are a digital object that provide proof of identity. Passwords, PINs, and biometric data
can all be used as credentials, depending on the application requirements.

* Tokens: Tokens are sometimes referred to as credentials though they are instead referred to as a digital object that
  proves that the caller provided proper credentials.

> For authentication and authorization, a token is a digital object that shows that a caller provided proper credentials
> that were exchanged for that token. The token contains information about the identity of the principal making the
> request and what kind of access they are authorized to make.
>
> Tokens can be thought of as being like hotel keys. When you check in to a hotel and present the proper documentation
> to the hotel registration desk, you receive a key that gives you access to specific hotel resources. For example, the
> key might give you access to your room and the guest elevator, but would not give you access to any other room or the
> service elevator.
>
> Except API keys, Google APIs do not support credentials directly. Your application must acquire or generate a token
> and
> provide it to the API. There are several different types of tokens. For more information, see Token types.

The type of credentials depends on where is being authenticated to:

* API Keys: Unlike other credentials, API keys do not identify a principal. API keys provide a Google Cloud project for
  billing and quota purposes.
* Oauth Client ID: OAuth Client IDs are used to identify an application to Google.

#### Principal

A principal is an identity that can be granted access to a resource. For authentication, Google APIs support two types
of principals: user accounts and service accounts.

1. User accounts: User accounts represent a developer, administrator, or any other person who interacts with Google APIs
   and services. User accounts are managed as Google Accounts, either with Google Workspace or Cloud Identity. They can
   also be user accounts that are managed by a third-party identity provider and federated with workforce identity
   federation.
2. Service accounts: Service accounts are accounts that do not represent a human user. They provide a way to manage
   authentication and authorization when a human is not directly involved, such as when an application needs to access
   Google Cloud resources. Service accounts are managed by IAM.

## What is Application Default Credentials ?

Application Default credential is strategy by the **Google Authentication Libraries** to automatically find credentials
based on the application environment. The authentication libraries then made it available to **Cloud Client Libraries
and
Google API Client Libraries**.

### Search order:

ADC searches for credentials in the following locations:

1. GOOGLE_APPLICATION_CREDENTIALS environment variable
2. User credentials set up by using the Google Cloud CLI
3. The attached service account, returned by the metadata server

##### GOOGLE_APPLICATION_CREDENTIALS environment variable

The environment variable can be used to provide the location of the credential JSON file. The JSON file can be of below
types

* A credential configuration file for workload identity federation
* A service account key
  > Service account keys create a security risk and are not recommended. Unlike the other credential file types,
  compromised service account keys can be used by a bad actor without any additional information.

> **User Credentials required by ADC can be provided by GCLOUD, by running gcloud auth application-default login
command.**
>
> The credentials provided to ADC by using the gcloud CLI are distinct from the gcloud credentials —the credentials the
> gcloud CLI uses to authenticate to Google Cloud. The local ADC contains the access and refresh tokens. Any user with
> access to your file system can use those credentials.


--- 
Links

* <https://cloud.google.com/docs/authentication>
* <https://cloud.google.com/docs/authentication/application-default-credentials>
