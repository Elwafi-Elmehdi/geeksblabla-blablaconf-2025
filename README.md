# Terraform

## Table of Contents
1. [Installation Instructions](#installation-instructions)
3. [Project Structure](#project-structure)
4. [Resources](#resources)

## Installation Instructions

1- Install Terraform (MacOS)

```shell
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/terraform
```

2- Generate `.terraform.rc` file
```shell
$ cat <<EOF > ~/.terraform.rc
plugin_cache_dir = "~/.terraform.d/plugin-cache"
EOF
```

3- Install Terraform Pre-Commit package

```shell
$ brew install pre-commit
```

4- Copy and modify the pre-commit config

```shell
$ nvim ./.pre-commit-config.yaml
  hooks:
    - id: terraform_validate
    - id: terraform_fmt
#   - add your favorite hooks here
```

5- Configure the pre-commit hook globally
```shell
DIR=~/.git-template
git config --global init.templateDir ${DIR}
pre-commit init-templatedir -t pre-commit ${DIR}
```

6- Install pre-commit to run each time a git commit is issued.
```shell
$ pre-commit install
```

7- Add terraform alias to your `.bashrc or .zshrc` file
```shell
cat <<EOF >> ~/.zshrc
alias tf=terraform
alias tfa='terraform apply'
alias tfc='terraform console'
alias tfd='terraform destroy'
alias tff='terraform fmt'
alias tfi='terraform init'
alias tfo='terraform output'
alias tfp='terraform plan'
alias tfv='terraform validate'
EOF 
```
## Project structure

the code is structured following order of per **provider**, per **region**, per **environment**, and per **product**. 
```
.
├── <provider>
    ├── <region>
        ├── <environment>
            ├── <product>
```

My recomanded project archetecture.

```
.
├── aws
│   └── eu-west-3
└── azure
    └── west-eu-3
        ├── prod
        │   ├── control-plane
        │   ├── data-plane
        │   ├── monitoring-stack
        │   ├── alarms
        │   └── vpc
        └── test
```

## Resources
- [Pre-Commit](https://pre-commit.com/#install)
- [Terraform Install Docs](https://developer.hashicorp.com/terraform/install)

