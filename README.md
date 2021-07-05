## argo workflows

Argo is more of a stateless operation if compared to Airflow.
Airflow keeps the state of each operation and saves the context of the operation which yields its pros and cons.

Airflow

pros

- context is saved, so we can get a glimpse of what happened and when it happened, and rerun that job once it is fixed
- batteries included, alot of operations are built in, such as the sftp hook or gcp hooks.

cons

- since it is context aware, most operations are not selfcontained and is therefore a bit harded to scale up and depend on the implemetation that airflow provides
- python focused, makes it hard for non-python devs to come in and work around airflow and its setup

Argo

pros

- events (notifications) and first-class api for the different jobs.
- UI
- scheduling was quite easy and with dag capabilities if we would like
- easy deploy, kubectl apply argo -f , so easy to handle upgrades (probably)

cons

- ALOT of yaml

## workflow

A workflow should be seen as a function or method in any programming language.
It is a spec that defines some operation that should be performed on top of some dag, sequence or cron operation.


## workflow template

Creates a workflow into the templates directory to be used by argo multiple times.

## cron workflow

A cron operator for the workflows that we specify

## secrets are not shared for argo namespace
We need to copy secrets from default to argo namespace to use them.

kubectl get secret gitlab-registry --namespace=revsys-com --export -o yaml |\
   kubectl apply --namespace=devspectrum-dev -f -
