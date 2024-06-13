# Local Testbed Setup

This document provides the local testbed setup configuration and other
related information as may be necessary for someone either administering
the setup or using it as a developer.

## Machine Details

- The servers assigned for the work are:

    1. Pluto (aka ``traffic-generator`` from now on) - 192.168.10.10
    2. Snitch (aka ``application-server`` from no on) - 192.168.10.16

- Each developer has a user created and assigned to them by the project lead.
- All developers belong to the ``dev`` group created on both servers.
- No developer has access to the ``root`` user and the privileges are
only available on a per-need basis, by consultation with the team and the
team lead.
- There is a ``/shared`` directory on both servers that can be used as a
common folder for all ``dev`` users to share files.
- The ``/shared/pcaps`` directory on the ``traffic-generator`` is to be used
to store all the capture files that will be used for testing.

Tip: You can create host names in your development machine to keep track of the
``traffic-generator`` and  ``application-server``.

## Jenkins Setup

The ``traffic-generator`` host is used as a Jenkins CI as well. It is setup
using ``docker compose`` as defined in the ``compose.yaml`` file. The file
is commented verbosely to help understand the setup.

Primarily, the CI consists of a ``docker-in-docker`` setup, to isolate
Jenkins ``docker agent`` jobs in a separate docker instance.

The ``Dockerfile.jenkins`` is used to generate the Jenkins image that helps
setup the infrastructure. It uses a Jenkins base image and sets up a few
plugins that are needed for this workflow. As we use more plugins in our setup
we will continue to modify this Dockerfile and update our infrastructure to
record these changes.

To work with the docker setup locally, developers will be assigned to the
``docker`` group on the ``traffic-generator`` host. This will allow them to
work with the docker daemon in a non-root user fashion, as per recommended
practices.

Jenkins CI will have developer user accounts allowing the developers to be
able to see the setup and interact with it as they develop code. The CI
setup is available on the following URL ``192.168.10.10:8080``.

Note: For inclusion in the ``docker`` group as well as a Jenkins user account,
you'll have to contact the project lead. **USER ACCOUNT SHARING IS NOT
RECOMMENDED**.
