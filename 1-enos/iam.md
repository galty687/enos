# User and access management

EnOS applies the identity and access management (IAM) scheme to support
multi-tenancy, where each tenant in the EnOS is managed as an organizational
unit, the data in different organizations are securely segregated and can only
be accessed by users that are registered to the organization.

The EnOS built-in IAM scheme provides capabilities of identity management,
authentication, authorization, and auditing.

## Identity Management

IAM introduced a hierarchy structure to represent the relationship existing in
organization administration. Each customer (which is called agency in DECADA)
and its sub-division is identified as an organizational unit (OU).

Identities have different types. User accounts are usually created for EnOS
portal users and other platform O&M staffs. Service accounts (a.k.a. App tokens)
are assigned to applications, which want to access EnOS service APIs or to be
executed in EnOS streaming data engine. Device identities are allocated for all
devices and edges connected to EnOS.

All identities shall be created under OUs. Each OU has a unique owner and some
optional administrators.

IAM also provides capability of integrating with external user registries that
supports LDAP, such as Windows Directory Service.

## Authentication

IAM service provides different authentication methods for different account
types.

User accounts are allowed to access EnOS portal with valid credential (user
identifier and password). Strong password with enough complexity may be enforce
by security policy managed by OU administrator. Multi-factor authentication is
also a configurable security option, which may require the users to pass extra
login authentication steps when enabled.

Service accounts uses access keys, which are digital signatures, to perform the
authentication with platform.

Devices and edges use X.509 certifications to establish the secure data
communication tunnels with EnOS cloud. Devices with TPM chips may store the
encrypted certifications in hardware.

EnOS implemented OAuth 2.0 to support SSO with external applications.

## Authorization

EnOS adopts Role-Based-Access-Control (RBAC) that is a policy neutral access
control mechanism defined around roles and privileges. Access control rule is
defined as a 3-tuples in the form of role-permission-resource.

[Roles](https://en.wikipedia.org/wiki/Role_(computer_science)) are created for
various job functions. Permissions to perform certain operations are assigned to
specific roles. Permission associated with roles can be defined on multiple
resources:

-   Applications – what kind of applications a role has access to

-   User Interface – what kind of menu items, or buttons a role can see

-   API – what kind of API a role can invoke

-   Data – what kind of data a role can read or write, such as wind farms,
    turbines, and sensors

-   Reports – what kind of reports a role can read

-   Alerts – what kind of application alerts a role can read or handle

IAM allows OU administrator to define access control rules to grant privileges
of resources to other accounts through IAM portal.

Accounts with proper privileges granted may access the corresponding resources
via EnOS service APIs or portal. Access control validation is performed by IAM
service for each access attempt. Success or failure attempts may be recorded by
IAM logging feature for auditing and abnormality detection purpose.

## Auditing

IAM provides auditing features to allow customer’s operation or security staffs
to review its user activity logs associated with their users and applications.
