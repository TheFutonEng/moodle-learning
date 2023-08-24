# moodle-learning
Learning about Moodle

The docker compose file out there by Bitnami spins up a web container and a database container.  The default credentials in the moodles docs of [admin/admin](https://docs.moodle.org/20/en/Installing_Moodle#:~:text=TIP%3A%20If%20for%20any%20reason,with%20password%20%22admin%22.)) do not work.

To spin up just the containers:

```bash
curl -sSL https://raw.githubusercontent.com/bitnami/containers/main/bitnami/moodle/docker-compose.yml > docker-compose.yml
docker-compose up -d
```

# Helm Chart
Going to mess around with the Helm chart next where admin credentials can be supplied in a `values.yaml` file.  First step is to spin up a K3d cluster:

```
k3d cluster create moodle -p "8081:80@loadbalancer" --agents 2
```

Then deploy Moodle via Helm:

```
kubectl create ns moodle
helm install moodle -n moodle oci://registry-1.docker.io/bitnamicharts/moodle -f values.yaml 
```