# Spec Check

This script is designed to list the changes in the releases used between two different versions of a genesis kit (or any BOSH manifest), and list any differences found in spec files between those release versions.

## Usage

It must be run from within the repo, and the previous version must be a tag or branch:

```
spec-check <branch|tag>
```

If not provided, it will compare against the `origin/master` branch.

## Output

The output will be a list of Removed, Unchanged, Added and Changed Releases, which any empty category being suppressed in the output.  Following those lists, if any changed releases exist, there will be a summary of job spec changes per release.

For example, here is the output between v1.9.1 and the release candidate for v1.10.0 for `genesis-community/cf-genesis-kit`

```
$ ~/bin/spec-check v1.9.1
Unchanged Releases:
  - app-autoscaler (2.0.0)
  - bosh-dns-aliases (0.0.3)
  - bpm (1.1.6)
  - capi (1.89.0)
  - cf-networking (2.27.0)
  - cflinuxfs2 (1.286.0)
  - garden-runc (1.19.9)
  - haproxy (9.7.1)
  - java-buildpack (4.26)
  - mapfs (1.2.0)
  - nats (32)
  - nfs-volume (2.3.0)
  - postgres (3.2.0)
  - routing (0.196.0)
  - silk (2.27.0)

Changed Releases:
  - binary-buildpack (1.0.35 -> 1.0.36)
  - cf-cli (1.23.0 -> 1.24.0)
  - cf-smoke-tests (40.0.123 -> 40.0.125)
  - cf-syslog-drain (10.2.7 -> 10.2.9)
  - cflinuxfs3 (0.151.0 -> 0.154.0)
  - diego (2.41.0 -> 2.42.0)
  - dotnet-core-buildpack (2.3.2 -> 2.3.3)
  - go-buildpack (1.9.3 -> 1.9.4)
  - log-cache (2.6.6 -> 2.6.8)
  - loggregator (106.3.1 -> 106.3.5)
  - loggregator-agent (5.3.1 -> 5.3.4)
  - nginx-buildpack (1.1.1 -> 1.1.3)
  - nodejs-buildpack (1.7.4 -> 1.7.8)
  - php-buildpack (4.4.2 -> 4.4.5)
  - python-buildpack (1.7.2 -> 1.7.5)
  - r-buildpack (1.1.0 -> 1.1.1)
  - ruby-buildpack (1.8.2 -> 1.8.6)
  - staticfile-buildpack (1.5.1 -> 1.5.3)
  - statsd-injector (1.11.10 -> 1.11.13)
  - uaa (74.12.0 -> 74.13.0)

Fetching spec diffs...
[binary-buildpack] No changes to spec files between 1.0.35 and 1.0.36

[cf-cli] No changes to spec files between 1.23.0 and 1.24.0

[cf-smoke-tests] No changes to spec files between 40.0.123 and 40.0.125

[cf-syslog-drain] No changes to spec files between 10.2.7 and 10.2.9

[cflinuxfs3] No changes to spec files between 0.151.0 and 0.154.0

[diego/job/rep] Change detected in spec file between 2.41.0 and 2.42.0
  $.properties.diego.executor.max_log_lines_per_second added
    default: 0
    description: 'EXPERIMENTAL: Maximum log lines allowed per second per app instance.
      Default value of 0 will disable rate limiting. Minimum recommended value is 100.'


[diego/job/rep_windows] Change detected in spec file between 2.41.0 and 2.42.0
  $.properties.diego.executor.max_log_lines_per_second added
    default: 0
    description: 'EXPERIMENTAL: Maximum log lines allowed per second per app instance.
      Default value of 0 will disable rate limiting. Minimum recommended value is 100.'



[dotnet-core-buildpack] No changes to spec files between 2.3.2 and 2.3.3

[go-buildpack] No changes to spec files between 1.9.3 and 1.9.4

[log-cache] No changes to spec files between 2.6.6 and 2.6.8

[loggregator/job/doppler] Change detected in spec file between 106.3.1 and 106.3.5
  $.properties.doppler.health_addr removed
    default: localhost:14825
    description: The host:port to expose health metrics for doppler

  $.templates.dns_health_check.erb changed value
    from bin/dns_health_check
      to bin/dns/healthy


[loggregator/job/loggregator_trafficcontroller] Change detected in spec file between 106.3.1 and 106.3.5
  $.properties.traffic_controller.health_addr removed
    default: localhost:14825
    description: The host:port to expose health metrics for trafficcontroller


[loggregator/job/reverse_log_proxy] Change detected in spec file between 106.3.1 and 106.3.5
  $.properties.reverse_log_proxy.health_addr removed
    default: localhost:0
    description: The host:port to expose health metrics for reverse log proxy



[loggregator-agent] No changes to spec files between 5.3.1 and 5.3.4

[nginx-buildpack] No changes to spec files between 1.1.1 and 1.1.3

[nodejs-buildpack] No changes to spec files between 1.7.4 and 1.7.8

[php-buildpack] No changes to spec files between 4.4.2 and 4.4.5

[python-buildpack] No changes to spec files between 1.7.2 and 1.7.5

[r-buildpack] No changes to spec files between 1.1.0 and 1.1.1

[ruby-buildpack] No changes to spec files between 1.8.2 and 1.8.6

[staticfile-buildpack] No changes to spec files between 1.5.1 and 1.5.3

[statsd-injector] No changes to spec files between 1.11.10 and 1.11.13

[uaa/job/uaa] Change detected in spec file between 74.12.0 and 74.13.0
  $.properties.uaa.ssl.port_header added
    default: X-Forwarded-Port
    description: The header to look for to determine the port where ssl termination was
      performed by a front end load balancer.
```

