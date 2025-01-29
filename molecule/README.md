# Molecule Tests

This directory contains some Ansible [`molecule`](https://ansible.readthedocs.io/projects/molecule/) test scenarios.

## Requirements

- Python >= 3.10
- ansible-core >= 2.12
- Molecule (see installation instructions below)
- Podman
- Container images (see [github.com/clifford2/molecule-containers](https://github.com/clifford2/molecule-containers) for examples)

You can install Molecule as follows:

```sh
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install molecule ansible-core
```

## Usage

This directory contains a **scenario** for each of our roles.

To run the tests, use the `molecule` subcommands below, and pass the name of the scenario to target with `-s <scenario>`.

Example:

```sh
molecule test -s gather-podman
```

You can use the `test` command to run all steps (create the target plaforms, run the tests, and destroy the platforms again).

During development, a more efficient approach might be to run the actions individually, as follows:

- `create` the platforms
- Use `converge` & `verify` for testing, repeating as often as required after code changes
- `destroy` when done

See the [Command Line Reference](https://ansible.readthedocs.io/projects/molecule/usage/) for a quick reference.

Key `molecule` commands:

```
create       Use the provisioner to start the instances.
list         List status of instances.
converge     Run the tests in your `converge.yml` playbook.
verify       Run automated tests against instances (`verify.yml`).
login        Log in to one instance.
destroy      Use the provisioner to destroy the instances.
```

## KubeVirt

Create a [Minikube](https://minikube.sigs.k8s.io/docs/start/) cluster, using [KVM](https://minikube.sigs.k8s.io/docs/drivers/kvm2/):

```sh
minikube start --profile minikube-molecule --driver=kvm2 --cpus=4 --memory=16384
```

Or create a Minikube cluster using [Docker](https://minikube.sigs.k8s.io/docs/drivers/docker/):

```sh
minikube start --profile minikube-molecule --driver=docker --cpus=4 --memory=16384
sudo sed -i.bak -e '/minikube-molecule/d' /etc/hosts
echo "$(minikube ip --profile minikube-molecule) minikube-molecule" | sudo tee -a /etc/hosts
```

Install KubeVirt (see <https://kubevirt.io/quickstart_minikube/>):

```sh
export KUBEVIRT_VERSION=$(curl -s https://storage.googleapis.com/kubevirt-prow/release/kubevirt/kubevirt/stable.txt)
echo $KUBEVIRT_VERSION
kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-operator.yaml"
kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-cr.yaml"
kubectl get kubevirt.kubevirt.io/kubevirt -n kubevirt -o=jsonpath="{.status.phase}" ; echo
kubectl get all -n kubevirt
```

Prepare host for Molecule:

```sh
python3 -m pip install -r shared/kubevirt-requirements.txt
kubectl apply -f molecule/shared/kubevirt-serviceaccount.yaml
```

To run Molecule, set appropriate `K8S_AUTH_*` environment variables per the [`kubernetes.core.k8s` module documentation](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/k8s_module.html), for example:

```sh
export K8S_AUTH_KUBECONFIG='~/.kube/config'
export K8S_AUTH_CONTEXT='minikube-molecule'
```

Once set, run molecule with:

```sh
molecule test -s gather-kubevirt
```
