# Nomad Job Example

This directory contains an example Nomad job specification (`example.nomad.hcl`) that deploys a Redis cache service.

## Prerequisites

- [Nomad](https://developer.hashicorp.com/nomad/docs/install) installed and running.
- [Docker](https://docs.docker.com/get-docker/) installed (since the example job uses the Docker driver).

## Usage

### 1. Validate the Job

Before running the job, you can validate the syntax of the job file:

```bash
nomad job validate example.nomad.hcl
```

### 2. Plan the Job

Run a plan to see what changes Nomad will make:

```bash
nomad job plan example.nomad.hcl
```

### 3. Run the Job

Submit the job to your Nomad cluster:

```bash
nomad job run example.nomad.hcl
```

### 4. Check Job Status

Verify the status of the job:

```bash
nomad job status example
```

To see the logs of the allocations:

```bash
nomad alloc logs <alloc-id>
```
(Replace `<alloc-id>` with the actual allocation ID from the status command).

### 5. Stop the Job

To stop and purge the job:

```bash
nomad job stop -purge example
```

## Job Details

- **Job Name**: `example`
- **Type**: `service`
- **Task Group**: `cache`
- **Task**: `redis` (uses `redis:7` Docker image)
- **Resources**: 500 MHz CPU, 256 MB Memory
- **Network**: Exposes port 6379 (mapped to `db` port)
