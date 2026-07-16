# Load Balancer

## Project Overview

This project is part of the **ALU System Engineering & DevOps** curriculum. It focuses on scaling a web infrastructure horizontally by introducing multiple web servers behind a load balancer, and automating server configuration using Bash scripting.

The goal is to move from a single web server setup to a distributed one, where traffic is spread across multiple identical servers. To achieve this in a repeatable, automated way, each configuration step is written as a Bash script rather than performed manually.

## Learning Objectives

By completing this project, the following concepts are covered:

- What a load balancer is and why it's used
- The difference between a web server, an application server, and a load balancer
- What an HTTP header is, and how to add a custom one to Nginx responses
- How to write idempotent, automated Bash scripts to configure servers
- How to verify server behavior using `curl`

## Requirements

- All scripts are written in Bash and tested on Ubuntu
- Every script starts with `#!/usr/bin/env bash`
- Scripts must pass [Shellcheck](https://www.shellcheck.net/) validation (unless a specific rule is explicitly allowed to be ignored, as noted in the task)
- All scripts must be executable
- Scripts must be written so they can configure a **brand new** Ubuntu machine from scratch (no assumptions about pre-installed packages)

## Tasks

### 0. Double the number of web servers

**File:** [`0-custom_http_response_header`](./0-custom_http_response_header)

This script configures a fresh Ubuntu machine so that Nginx returns a custom HTTP response header, `X-Served-By`, whose value is the hostname of the server. This makes it possible to identify which web server answered a given request — a key requirement once a load balancer is placed in front of multiple servers.

**What it does:**
1. Installs Nginx if it isn't already installed
2. Retrieves the server's hostname
3. Inserts an `add_header X-Served-By <hostname>;` directive into the Nginx configuration
4. Restarts Nginx to apply the change

**Usage:**
```bash
sudo bash 0-custom_http_response_header
```

**Verification:**
```bash
curl -sI <server-ip> | grep X-Served-By
# Example output:
# X-Served-By: 03-web-01
```

This script is run on both `web-01` and `web-02` so that each server identifies itself uniquely in its HTTP responses.

## Repository

- **GitHub repository:** `alu-system_engineering-devops`
- **Directory:** `load_balancer`

## Author

Written as part of the ALU System Engineering / DevOps track.
