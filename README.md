alb_route53
=========


Requirements
------------

Add these role git url to requirements.yml for ansible galaxy to work

aws_route53 - ssh://git@bitbucket.xvt.technology:7999/xans/aws_route53.git
aws_profile_account - ssh://git@bitbucket.xvt.technology:7999/xans/aws_profile_account.git

Role Variables
--------------
- `load_balancer_name` - required - no default
  The load_balancer_name to create DNS for

- `aws_route53_profile_public` - optional - no default
  The aws profile that we are going to create the public route53 entry. If not
  provided then fall back to use IAM profile. See
  https://bitbucket.xvt.technology/projects/XANS/repos/aws_route53/browse for
  more.

- `alb_route53_dns` - Optional - Default: `role_type`.`tld_name_external`
  The dns record that this role is going to create and will have the value of the `load_balancer_name`.`domain_name`.

- `tld_name_external` - the public zone name.

- `role_type` - role type - required if `alb_route53_dns` is not provided.

The DNS will be created as a CNAME of the alb and the value is <role_type>.<tld_name_external>

Dependencies
------------

role: aws_route53
      to do the actual route53 request

role: aws_profile_account
      to handle the case when we are running in ec2 which has the IAM profile
      that can assume the target route53_admin IAM role in the aws account that
      we create the entry.
      This eliminates the need to use the local target aws account profile.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
