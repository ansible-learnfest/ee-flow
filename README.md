## Checkout repo
Clone the repo to your VS Code terminal
```
git clone https://github.com/ansible-learnfest/ee-flow.git
```

## Login to registry.redhat.io
```
podman login registry.redhat.io
```

## Build EE
* In the repo change to the `ansible-builder` directory
* Run `ansible-builder build -f ee-ansible-demo.yml -t ee-ansible-demo:0.1.0 -v 3`

## Push image to PAH
```
podman login pah.<LABID>.<SUBDOMAIN>.opentlc.com --username admin --password XXXXX
podman tag localhost/ee-ansible-demo:0.1.0 pah.<LABID>.<SUBDOMAIN>.opentlc.com/ee-ansible-demo:latest
podman push localhost/ee-ansible-demo:0.1.0 pah.<LABID>.<SUBDOMAIN>.opentlc.com/ee-ansible-demo
```

## Configure EE in Controller
- Check the **Credential** Automation Hub Container Registry points to the PAH
- Go to `Execution Environments`
- Configure the new EE
  - **Name**: ee-ansible-demo
  - **Image**: pah.<LABID>.<SUBDOMAIN>.opentlc.com/ee-ansible-demo:latest
  - **Credential**: Automation Hub Container Registry

## Create Project
- Create a new Project to point to https://github.com/ansible-learnfest/ee-flow.git

## Create Credentials
  
## Create Inventory
  
## Create Job Template
- Create a new Job Template `Deploy Container` that
  - Runs deploy-container.yml from the new Project
  - Uses the new EE with the Podman collection

Run the Job Template

## Check
From the VSCode Terminal: `curl node1.<LABID>.internal`
