# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

_Public Classes_

* [`fetchcrl`](#fetchcrl): Main class, installs fetch-crl and configured it.
https://wiki.nikhef.nl/grid/FetchCRL3

_Private Classes_

* `fetchcrl::config`: Configures fetch-crl
* `fetchcrl::install`: Installs fetch-crl
* `fetchcrl::service`: Controls fetch-crl cron and startup

**Defined types**

* [`fetchcrl::ca`](#fetchcrlca): Creates per CA configuration files.

## Classes

### fetchcrl

fetchcrl

#### Examples

##### 

```puppet
class{'fetchcrl':
  http_proxy            => 'http:://squid.example.org:8000',
  carepo                => 'http://yum.example.org/yumrepo',
  cache_control_request => '3600',
}
```

#### Parameters

The following parameters are available in the `fetchcrl` class.

##### `capkgs`

Data type: `Array[String[1]]`

CA policy packages to install.

Default value: ['ca-policy-egi-core']

##### `carepo`

Data type: `Stdlib::Httpurl`

Repository URL of CA packages.

Default value: 'http://repository.egi.eu/sw/production/cas/1/current/'

##### `manage_carepo`

Data type: `Boolean`

Should package repository be configured.

Default value: `true`

##### `capkgs_version`

Data type: `String`

Version of CA packages.

Default value: 'present'

##### `pkg_version`

Data type: `String`

Version of fetch-crl package.

Default value: 'present'

##### `agingtolerance`

Data type: `Integer`

Number of hours delay time before errors are generated in case downloads consistently fail.

Default value: 24

##### `nosymlinks`

Data type: `Boolean`

do not create serial number symlinks.

Default value: `true`

##### `noerrors`

Data type: `Boolean`

do not produce errors.

Default value: `false`

##### `nowarnings`

Data type: `Boolean`

do not produce warnings.

Default value: `true`

##### `http_proxy`

Data type: `Optional[Stdlib::Httpurl]`

List of http proxy URLs.

Default value: `undef`

##### `httptimeout`

Data type: `Integer`

Time out for http.

Default value: 30

##### `parallelism`

Data type: `Integer`

Number of fetchs to run concurrently.

Default value: 4

##### `logmode`

Data type: `Enum['direct','qualified',
        'cache','syslog']`

Specify how logging is done.

Default value: 'syslog'

##### `pkgname`

Data type: `String[1]`

Name of fetch-crl package.

Default value: 'fetch-crl'

##### `runcron`

Data type: `Boolean`

Should fetch-crl be run as a cron job.

Default value: `true`

##### `runboot`

Data type: `Boolean`

Should fetch-crl be run at boot time.
This parameter is only significant for fetch-crl packages
that do not use a cron based package and not a systemd timer.

Default value: `false`

##### `randomcron`

Data type: `Boolean`

Should the every 6 hour cron be configured with a random offset.
With osfamily RedHat 8 or newer the randomcron parameter is ignored.
The systemd timer for fetch-crl is already very random.

Default value: `true`

##### `cache_control_request`

Data type: `Optional[Integer]`

sends a cache-control max-age hint in seconds towards the server in the HTTP request.

Default value: `undef`

## Defined types

### fetchcrl::ca

Creates per CA configuration files.

#### Examples

##### 

```puppet
fetchcrl::ca{'EDG-Tutorial-CA':
  agingtolerance => 168
}
```

#### Parameters

The following parameters are available in the `fetchcrl::ca` defined type.

##### `name`

The name of the CA to manage a configuration for.

##### `anchorname`

Data type: `String[1]`

The name of the CA to manage a configuration for.

Default value: $title

##### `nowarnings`

Data type: `Boolean`

Should warnings be supressed for this CA.

Default value: `false`

##### `noerrors`

Data type: `Boolean`

Should errors be supressed for this CA.

Default value: `false`

##### `httptimeout`

Data type: `Optional[Integer]`

The timeout for this CA.

Default value: `undef`

##### `agingtolerance`

Data type: `Optional[Integer]`

The delay if failures before it is considered an error.

Default value: `undef`

##### `crl_url`

Data type: `Array[Stdlib::Httpurl]`

A list of URLs to download CAs from

Default value: []

