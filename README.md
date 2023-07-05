# Docker images with systemd for molecule

You can use these images as base containers to run systemd services inside. Normally you wouldn't do this. But if you want to test your Ansible roles with [molecule](https://ansible.readthedocs.io/projects/molecule/) it is pretty handy to have a docker container running with systemd. This allows you to also test systemd tasks (e.g. restart of a service) you typically need on your physical hosts.

## Usage

See the README file in the distribution folder you want to use.
