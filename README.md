# gha-deployment-example

Configurable deployment scripts example using GitHub Actions. Very basic example of a set of reusable actions and workflows to perform deployments of:
- Multiple service
- Multiple environments
- For multiple customers
from a centralised deployments repo.

## Assumptions

- Each service has the same Path to Live through a set of environments (e.g. QA -> Staging -> Production)
- Each service produces and promotes an artifact in the same way (e.g. dev -> alpha -> beta -> final)
- Production of the original artifact (dev) happens outside of this pipeline

## Workflows

### main

Entry point workflow for a push to prod. Contains a job which activates the reuseable workflow `service-deployment.yaml` for each service you want to deploy.

### service-deployment

Control flow for a single service. Makes use of the `deployment-environment` and `release-artifact` custom actions for consistent deployments through your Path to Live. Inputs allow configuration per customer, so if you have some services that are customer specific it will ignore those environments. It also enforces that an artifact has been produced for a deployment before it will let you perform that deployment. Deployments are gated on environments.

## Actions

### release-artifact

Dummy action - takes some configuration and pretends to promote an artifact from one level to the next (e.g. alpha to beta).

### deploy-environment

Dummy action - takes an artifact (e.g. alpha) and deploys it to an environment.
