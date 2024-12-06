# DeployAwxOnK8s

Rendez-vous sur le projet github d'awx operator:

```bash
https://github.com/ansible/awx-operator
```

Et installer au sein de votre cluster 'awx-operator':

```
cd awx-operator
make deploy
```

Puis installer l'ui awx:

```bash
ansible-playbook ansible/instantiate-awx-deployment.yml \ 
    -e development_mode=no -e image=ghcr.io/ansible/awx \
    -e image_version=24.0.0 -e image_pull_policy=Always \
    -e ansible_python_interpreter=/usr/bin/python3 -e service_type=nodeport \ 
    -e namespace=awx     -e nodeport_port=30080
```

Important: `nodeport_port` est mal interpreter par ansible il va falloir modifier le fichier `ansible/instantiate-awx-deployment.yml` dans `awx-operator`.

