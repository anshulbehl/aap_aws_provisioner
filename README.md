# Deploy AAP21 on AWS using Ansible

- An `offline_token` is required for downloading the AAP bundle. Put this value into the `vars.yml` file below. See https://github.com/ansible/workshops/tree/devel/roles/aap_download for more details. Generate a token here: https://access.redhat.com/management/api.

- Prerequisites

  ```
  # Copy and edit the variables file
  cp vars.yml.sample vars.yml
  # vim vars.yml

  # Install Python dependencies
  pip install -r requirements.txt

  # Install Ansible Collection dependencies
  ansible-galaxy collection install -r collections/requirements.yml

  # Export AWS credentials
  export AWS_ACCESS_KEY_ID='AK123'
  export AWS_SECRET_ACCESS_KEY='abc123'
  ```

- Run playbook

  ```
  ansible-playbook -e @vars.yml provision.yml
  ```

  You should be able to SSH to the created instance with:

  ```
  ssh -i <prefix>/<prefix>-private.pem ec2-user@<ip>
  ```

- Teardown

  ```
  ansible-playbook -e @vars.yml teardown.yml
  ```

- In the event of the provision playbook failing, it is advised to run the teardown playbook before re-trying. Otherwise you might end up with duplicate resources, within the created VPC, that will need to be manually cleaned.
