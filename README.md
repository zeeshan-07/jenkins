# 2G/3G Whitelisting Solution

The WL solution performs packet capture, does correlation of user identity
with stream identity, and filters whitelisted user (signalling+data) streams
from the incoming traffic.

The solution has 2 parts:

1. The core WL golang application.
2. The GUI Dashboard for statistics and basic interaction with the application
through an API.

## The Repository Structure

The repository has primarily the following directories:

1. app - The parent directory for the golang application.
2. dashboard - The parent directory for the dashboard web application.
3. docs - The parent directory that houses the project design documentation.

## Some Recommendation

- For linting documentation, it is recommended to use a markdown lint extension
in VSCode.
