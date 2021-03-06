# 😽 kitten

[![Build Status](https://travis-ci.org/hoffa/kitten.svg?branch=master)](https://travis-ci.org/hoffa/kitten) [![Maintainability](https://api.codeclimate.com/v1/badges/34e6b84000b2ab0e1bce/maintainability)](https://codeclimate.com/github/hoffa/kitten/maintainability) [![PyPI - Python Version](https://svgshare.com/i/6tK.svg)](https://pypi.org/project/kitten)

Tiny multi-server automation tool.

It's designed to be as simple as possible and play nice with Unix tools.

![Screenshot](https://i.imgur.com/Qtx2WyC.png)

## Install

```Shell
pip install kitten
```

## Prerequisites

Kitten can get IP addresses from AWS resources for you. For that you'll need to have your AWS credentials set up. You can do that using `awscli`:

```Shell
pip install awscli
```

Then:

```Shell
aws configure
```

## Examples

### Get IP addresses from AWS resources

Use `kitten ip` with either `id`, `asg`, `elb` or `opsworks`:

```Shell
$ kitten ip id i-04703bf3e6fab1926 i-07f234d0f29113ef2
18.135.117.17
24.129.235.48
```

You can change region using `--region`.

By default only private IP addresses are printed. Use `--public` if you prefer public IPs.

### Run command on servers

```Shell
$ kitten run uptime ubuntu 18.105.107.20 34.229.135.48
18.105.107.20	run	uptime
34.229.135.48	run	uptime
18.105.107.20	17:11:48 up 1 day,  6:02,  0 users,  load average: 0.91, 2.99, 3.49
34.229.135.48	17:11:48 up 5 days, 11:19,  0 users,  load average: 6.34, 5.94, 5.72
```

Replace `ubuntu` with the user used to log in on the servers.

Commands are always run in parallel. Use `--threads` to specify the maximum number of concurrent connections (defaults to 10).

Use `--sudo` to run commands via `sudo`.

Use `-i` to specify a private key.

### Download files

```Shell
kitten ip opsworks a283c671-d4c1-4dfa-a7c2-823b7f7b2c2c | xargs kitten get /tmp/system.log ubuntu
```

### Upload file

```Shell
kitten ip asg big-prod-asg | xargs kitten put cat.jpg /root/cat.jpg root
```
