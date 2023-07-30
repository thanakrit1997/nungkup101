# nungkup101

Terraform module to deploy Kubernetes addons on Amazon EKS clusters.

## Usage

```hcl
module "eks" {
  source = "terraform-aws-modules/eks/aws"

  cluster_name    = "my-cluster"
  cluster_version = "1.27"

  ... truncated for brevity
}

module "eks_blueprints_addons" {
  source = "aws-ia/eks-blueprints-addons/aws"
  version = "~> 1.0" #ensure to update this to the latest/desired version

  cluster_name      = module.eks.cluster_name
  cluster_endpoint  = module.eks.cluster_endpoint
  cluster_version   = module.eks.cluster_version
  oidc_provider_arn = module.eks.oidc_provider_arn

  eks_addons = {
    aws-ebs-csi-driver = {
      most_recent = true
    }
    coredns = {
      most_recent = true
    }
    vpc-cni = {
      most_recent = true
    }
    kube-proxy = {
      most_recent = true
    }
  }

  enable_aws_load_balancer_controller    = true
  enable_cluster_proportional_autoscaler = true
  enable_karpenter                       = true
  enable_kube_prometheus_stack           = true
  enable_metrics_server                  = true
  enable_external_dns                    = true
  enable_cert_manager                    = true
  cert_manager_route53_hosted_zone_arns  = ["arn:aws:route53:::hostedzone/XXXXXXXXXXXXX"]

  tags = {
    Environment = "dev"
  }
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

| Name                                                                        | Version |
| --------------------------------------------------------------------------- | ------- |
| <a name="requirement_terraform"></a> [terraform](#requirement_terraform)    | >= 1.0  |
| <a name="requirement_aws"></a> [aws](#requirement_aws)                      | >= 5.0  |
| <a name="requirement_helm"></a> [helm](#requirement_helm)                   | >= 2.9  |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement_kubernetes) | >= 2.20 |
| <a name="requirement_time"></a> [time](#requirement_time)                   | >= 0.9  |

## Providers

| Name                                                                  | Version |
| --------------------------------------------------------------------- | ------- |
| <a name="provider_aws"></a> [aws](#provider_aws)                      | >= 5.0  |
| <a name="provider_helm"></a> [helm](#provider_helm)                   | >= 2.9  |
| <a name="provider_kubernetes"></a> [kubernetes](#provider_kubernetes) | >= 2.20 |
| <a name="provider_time"></a> [time](#provider_time)                   | >= 0.9  |

## Modules

| Name                                                                                                                                               | Source                          | Version |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | ------- |
| <a name="module_argo_events"></a> [argo_events](#module_argo_events)                                                                               | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_argo_rollouts"></a> [argo_rollouts](#module_argo_rollouts)                                                                         | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_argo_workflows"></a> [argo_workflows](#module_argo_workflows)                                                                      | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_argocd"></a> [argocd](#module_argocd)                                                                                              | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_cloudwatch_metrics"></a> [aws_cloudwatch_metrics](#module_aws_cloudwatch_metrics)                                              | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_efs_csi_driver"></a> [aws_efs_csi_driver](#module_aws_efs_csi_driver)                                                          | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_for_fluentbit"></a> [aws_for_fluentbit](#module_aws_for_fluentbit)                                                             | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_fsx_csi_driver"></a> [aws_fsx_csi_driver](#module_aws_fsx_csi_driver)                                                          | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_gateway_api_controller"></a> [aws_gateway_api_controller](#module_aws_gateway_api_controller)                                  | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_load_balancer_controller"></a> [aws_load_balancer_controller](#module_aws_load_balancer_controller)                            | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_node_termination_handler"></a> [aws_node_termination_handler](#module_aws_node_termination_handler)                            | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_aws_node_termination_handler_sqs"></a> [aws_node_termination_handler_sqs](#module_aws_node_termination_handler_sqs)                | terraform-aws-modules/sqs/aws   | 4.0.1   |
| <a name="module_aws_privateca_issuer"></a> [aws_privateca_issuer](#module_aws_privateca_issuer)                                                    | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_cert_manager"></a> [cert_manager](#module_cert_manager)                                                                            | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_cluster_autoscaler"></a> [cluster_autoscaler](#module_cluster_autoscaler)                                                          | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_cluster_proportional_autoscaler"></a> [cluster_proportional_autoscaler](#module_cluster_proportional_autoscaler)                   | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_external_dns"></a> [external_dns](#module_external_dns)                                                                            | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_external_secrets"></a> [external_secrets](#module_external_secrets)                                                                | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_gatekeeper"></a> [gatekeeper](#module_gatekeeper)                                                                                  | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_ingress_nginx"></a> [ingress_nginx](#module_ingress_nginx)                                                                         | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_karpenter"></a> [karpenter](#module_karpenter)                                                                                     | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_karpenter_sqs"></a> [karpenter_sqs](#module_karpenter_sqs)                                                                         | terraform-aws-modules/sqs/aws   | 4.0.1   |
| <a name="module_kube_prometheus_stack"></a> [kube_prometheus_stack](#module_kube_prometheus_stack)                                                 | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_metrics_server"></a> [metrics_server](#module_metrics_server)                                                                      | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_secrets_store_csi_driver"></a> [secrets_store_csi_driver](#module_secrets_store_csi_driver)                                        | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_secrets_store_csi_driver_provider_aws"></a> [secrets_store_csi_driver_provider_aws](#module_secrets_store_csi_driver_provider_aws) | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_velero"></a> [velero](#module_velero)                                                                                              | aws-ia/eks-blueprints-addon/aws | 1.1.0   |
| <a name="module_vpa"></a> [vpa](#module_vpa)                                                                                                       | aws-ia/eks-blueprints-addon/aws | 1.1.0   |

## Resources

| Name                                                                                                                                                                  | Type        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| [aws_autoscaling_group_tag.aws_node_termination_handler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_group_tag)           | resource    |
| [aws_autoscaling_lifecycle_hook.aws_node_termination_handler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_lifecycle_hook) | resource    |
| [aws_cloudwatch_event_rule.aws_node_termination_handler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_rule)           | resource    |
| [aws_cloudwatch_event_rule.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_rule)                              | resource    |
| [aws_cloudwatch_event_target.aws_node_termination_handler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_target)       | resource    |
| [aws_cloudwatch_event_target.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_target)                          | resource    |
| [aws_cloudwatch_log_group.aws_for_fluentbit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_group)                        | resource    |
| [aws_cloudwatch_log_group.fargate_fluentbit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_group)                        | resource    |
| [aws_eks_addon.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_addon)                                                           | resource    |
| [aws_iam_instance_profile.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile)                                | resource    |
| [aws_iam_policy.fargate_fluentbit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy)                                            | resource    |
| [aws_iam_role.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role)                                                        | resource    |
| [aws_iam_role_policy_attachment.additional](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment)                   | resource    |
| [aws_iam_role_policy_attachment.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment)                    | resource    |
| [helm_release.this](https://registry.terraform.io/providers/hashicorp/helm/latest/docs/resources/release)                                                             | resource    |
| [kubernetes_config_map_v1.aws_logging](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/config_map_v1)                              | resource    |
| [kubernetes_namespace_v1.aws_observability](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/namespace_v1)                          | resource    |
| [time_sleep.this](https://registry.terraform.io/providers/hashicorp/time/latest/docs/resources/sleep)                                                                 | resource    |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)                                         | data source |
| [aws_eks_addon_version.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_addon_version)                                        | data source |
| [aws_iam_policy_document.aws_efs_csi_driver](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                      | data source |
| [aws_iam_policy_document.aws_for_fluentbit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                       | data source |
| [aws_iam_policy_document.aws_fsx_csi_driver](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                      | data source |
| [aws_iam_policy_document.aws_gateway_api_controller](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)              | data source |
| [aws_iam_policy_document.aws_load_balancer_controller](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)            | data source |
| [aws_iam_policy_document.aws_node_termination_handler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)            | data source |
| [aws_iam_policy_document.aws_privateca_issuer](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                    | data source |
| [aws_iam_policy_document.cert_manager](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                            | data source |
| [aws_iam_policy_document.cluster_autoscaler](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                      | data source |
| [aws_iam_policy_document.external_dns](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                            | data source |
| [aws_iam_policy_document.external_secrets](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                        | data source |
| [aws_iam_policy_document.fargate_fluentbit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                       | data source |
| [aws_iam_policy_document.karpenter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                               | data source |
| [aws_iam_policy_document.karpenter_assume_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                   | data source |
| [aws_iam_policy_document.velero](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                                  | data source |
| [aws_partition.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/partition)                                                     | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region)                                                           | data source |

## Inputs

| Name                                                                                                                                                                  | Description                                                                                                                 | Type           | Default                                                     | Required |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | -------------- | ----------------------------------------------------------- | :------: |
| <a name="input_argo_events"></a> [argo_events](#input_argo_events)                                                                                                    | Argo Events add-on configuration values                                                                                     | `any`          | `{}`                                                        |    no    |
| <a name="input_argo_rollouts"></a> [argo_rollouts](#input_argo_rollouts)                                                                                              | Argo Rollouts add-on configuration values                                                                                   | `any`          | `{}`                                                        |    no    |
| <a name="input_argo_workflows"></a> [argo_workflows](#input_argo_workflows)                                                                                           | Argo Workflows add-on configuration values                                                                                  | `any`          | `{}`                                                        |    no    |
| <a name="input_argocd"></a> [argocd](#input_argocd)                                                                                                                   | ArgoCD add-on configuration values                                                                                          | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_cloudwatch_metrics"></a> [aws_cloudwatch_metrics](#input_aws_cloudwatch_metrics)                                                                   | Cloudwatch Metrics add-on configuration values                                                                              | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_efs_csi_driver"></a> [aws_efs_csi_driver](#input_aws_efs_csi_driver)                                                                               | EFS CSI Driver add-on configuration values                                                                                  | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_for_fluentbit"></a> [aws_for_fluentbit](#input_aws_for_fluentbit)                                                                                  | AWS Fluentbit add-on configurations                                                                                         | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_for_fluentbit_cw_log_group"></a> [aws_for_fluentbit_cw_log_group](#input_aws_for_fluentbit_cw_log_group)                                           | AWS Fluentbit CloudWatch Log Group configurations                                                                           | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_fsx_csi_driver"></a> [aws_fsx_csi_driver](#input_aws_fsx_csi_driver)                                                                               | FSX CSI Driver add-on configuration values                                                                                  | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_gateway_api_controller"></a> [aws_gateway_api_controller](#input_aws_gateway_api_controller)                                                       | AWS Gateway API Controller add-on configuration values                                                                      | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_load_balancer_controller"></a> [aws_load_balancer_controller](#input_aws_load_balancer_controller)                                                 | AWS Load Balancer Controller add-on configuration values                                                                    | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_node_termination_handler"></a> [aws_node_termination_handler](#input_aws_node_termination_handler)                                                 | AWS Node Termination Handler add-on configuration values                                                                    | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_node_termination_handler_asg_arns"></a> [aws_node_termination_handler_asg_arns](#input_aws_node_termination_handler_asg_arns)                      | List of Auto Scaling group ARNs that AWS Node Termination Handler will monitor for EC2 events                               | `list(string)` | `[]`                                                        |    no    |
| <a name="input_aws_node_termination_handler_sqs"></a> [aws_node_termination_handler_sqs](#input_aws_node_termination_handler_sqs)                                     | AWS Node Termination Handler SQS queue configuration values                                                                 | `any`          | `{}`                                                        |    no    |
| <a name="input_aws_privateca_issuer"></a> [aws_privateca_issuer](#input_aws_privateca_issuer)                                                                         | AWS PCA Issuer add-on configurations                                                                                        | `any`          | `{}`                                                        |    no    |
| <a name="input_cert_manager"></a> [cert_manager](#input_cert_manager)                                                                                                 | cert-manager add-on configuration values                                                                                    | `any`          | `{}`                                                        |    no    |
| <a name="input_cert_manager_route53_hosted_zone_arns"></a> [cert_manager_route53_hosted_zone_arns](#input_cert_manager_route53_hosted_zone_arns)                      | List of Route53 Hosted Zone ARNs that are used by cert-manager to create DNS records                                        | `list(string)` | <pre>[<br> "arn:aws:route53:::hostedzone/*"<br>]</pre>      |    no    |
| <a name="input_cluster_autoscaler"></a> [cluster_autoscaler](#input_cluster_autoscaler)                                                                               | Cluster Autoscaler add-on configuration values                                                                              | `any`          | `{}`                                                        |    no    |
| <a name="input_cluster_endpoint"></a> [cluster_endpoint](#input_cluster_endpoint)                                                                                     | Endpoint for your Kubernetes API server                                                                                     | `string`       | n/a                                                         |   yes    |
| <a name="input_cluster_name"></a> [cluster_name](#input_cluster_name)                                                                                                 | Name of the EKS cluster                                                                                                     | `string`       | n/a                                                         |   yes    |
| <a name="input_cluster_proportional_autoscaler"></a> [cluster_proportional_autoscaler](#input_cluster_proportional_autoscaler)                                        | Cluster Proportional Autoscaler add-on configurations                                                                       | `any`          | `{}`                                                        |    no    |
| <a name="input_cluster_version"></a> [cluster_version](#input_cluster_version)                                                                                        | Kubernetes `<major>.<minor>` version to use for the EKS cluster (i.e.: `1.24`)                                              | `string`       | n/a                                                         |   yes    |
| <a name="input_create_delay_dependencies"></a> [create_delay_dependencies](#input_create_delay_dependencies)                                                          | Dependency attribute which must be resolved before starting the `create_delay_duration`                                     | `list(string)` | `[]`                                                        |    no    |
| <a name="input_create_delay_duration"></a> [create_delay_duration](#input_create_delay_duration)                                                                      | The duration to wait before creating resources                                                                              | `string`       | `"30s"`                                                     |    no    |
| <a name="input_eks_addons"></a> [eks_addons](#input_eks_addons)                                                                                                       | Map of EKS add-on configurations to enable for the cluster. Add-on name can be the map keys or set with `name`              | `any`          | `{}`                                                        |    no    |
| <a name="input_eks_addons_timeouts"></a> [eks_addons_timeouts](#input_eks_addons_timeouts)                                                                            | Create, update, and delete timeout configurations for the EKS add-ons                                                       | `map(string)`  | `{}`                                                        |    no    |
| <a name="input_enable_argo_events"></a> [enable_argo_events](#input_enable_argo_events)                                                                               | Enable Argo Events add-on                                                                                                   | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_argo_rollouts"></a> [enable_argo_rollouts](#input_enable_argo_rollouts)                                                                         | Enable Argo Rollouts add-on                                                                                                 | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_argo_workflows"></a> [enable_argo_workflows](#input_enable_argo_workflows)                                                                      | Enable Argo workflows add-on                                                                                                | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_argocd"></a> [enable_argocd](#input_enable_argocd)                                                                                              | Enable Argo CD Kubernetes add-on                                                                                            | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_cloudwatch_metrics"></a> [enable_aws_cloudwatch_metrics](#input_enable_aws_cloudwatch_metrics)                                              | Enable AWS Cloudwatch Metrics add-on for Container Insights                                                                 | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_efs_csi_driver"></a> [enable_aws_efs_csi_driver](#input_enable_aws_efs_csi_driver)                                                          | Enable AWS EFS CSI Driver add-on                                                                                            | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_for_fluentbit"></a> [enable_aws_for_fluentbit](#input_enable_aws_for_fluentbit)                                                             | Enable AWS for FluentBit add-on                                                                                             | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_fsx_csi_driver"></a> [enable_aws_fsx_csi_driver](#input_enable_aws_fsx_csi_driver)                                                          | Enable AWS FSX CSI Driver add-on                                                                                            | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_gateway_api_controller"></a> [enable_aws_gateway_api_controller](#input_enable_aws_gateway_api_controller)                                  | Enable AWS Gateway API Controller add-on                                                                                    | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_load_balancer_controller"></a> [enable_aws_load_balancer_controller](#input_enable_aws_load_balancer_controller)                            | Enable AWS Load Balancer Controller add-on                                                                                  | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_node_termination_handler"></a> [enable_aws_node_termination_handler](#input_enable_aws_node_termination_handler)                            | Enable AWS Node Termination Handler add-on                                                                                  | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_aws_privateca_issuer"></a> [enable_aws_privateca_issuer](#input_enable_aws_privateca_issuer)                                                    | Enable AWS PCA Issuer                                                                                                       | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_cert_manager"></a> [enable_cert_manager](#input_enable_cert_manager)                                                                            | Enable cert-manager add-on                                                                                                  | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_cluster_autoscaler"></a> [enable_cluster_autoscaler](#input_enable_cluster_autoscaler)                                                          | Enable Cluster autoscaler add-on                                                                                            | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_cluster_proportional_autoscaler"></a> [enable_cluster_proportional_autoscaler](#input_enable_cluster_proportional_autoscaler)                   | Enable Cluster Proportional Autoscaler                                                                                      | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_external_dns"></a> [enable_external_dns](#input_enable_external_dns)                                                                            | Enable external-dns operator add-on                                                                                         | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_external_secrets"></a> [enable_external_secrets](#input_enable_external_secrets)                                                                | Enable External Secrets operator add-on                                                                                     | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_fargate_fluentbit"></a> [enable_fargate_fluentbit](#input_enable_fargate_fluentbit)                                                             | Enable Fargate FluentBit add-on                                                                                             | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_gatekeeper"></a> [enable_gatekeeper](#input_enable_gatekeeper)                                                                                  | Enable Gatekeeper add-on                                                                                                    | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_ingress_nginx"></a> [enable_ingress_nginx](#input_enable_ingress_nginx)                                                                         | Enable Ingress Nginx                                                                                                        | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_karpenter"></a> [enable_karpenter](#input_enable_karpenter)                                                                                     | Enable Karpenter controller add-on                                                                                          | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_kube_prometheus_stack"></a> [enable_kube_prometheus_stack](#input_enable_kube_prometheus_stack)                                                 | Enable Kube Prometheus Stack                                                                                                | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_metrics_server"></a> [enable_metrics_server](#input_enable_metrics_server)                                                                      | Enable metrics server add-on                                                                                                | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_secrets_store_csi_driver"></a> [enable_secrets_store_csi_driver](#input_enable_secrets_store_csi_driver)                                        | Enable CSI Secrets Store Provider                                                                                           | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_secrets_store_csi_driver_provider_aws"></a> [enable_secrets_store_csi_driver_provider_aws](#input_enable_secrets_store_csi_driver_provider_aws) | Enable AWS CSI Secrets Store Provider                                                                                       | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_velero"></a> [enable_velero](#input_enable_velero)                                                                                              | Enable Kubernetes Dashboard add-on                                                                                          | `bool`         | `false`                                                     |    no    |
| <a name="input_enable_vpa"></a> [enable_vpa](#input_enable_vpa)                                                                                                       | Enable Vertical Pod Autoscaler add-on                                                                                       | `bool`         | `false`                                                     |    no    |
| <a name="input_external_dns"></a> [external_dns](#input_external_dns)                                                                                                 | external-dns add-on configuration values                                                                                    | `any`          | `{}`                                                        |    no    |
| <a name="input_external_dns_route53_zone_arns"></a> [external_dns_route53_zone_arns](#input_external_dns_route53_zone_arns)                                           | List of Route53 zones ARNs which external-dns will have access to create/manage records (if using Route53)                  | `list(string)` | `[]`                                                        |    no    |
| <a name="input_external_secrets"></a> [external_secrets](#input_external_secrets)                                                                                     | External Secrets add-on configuration values                                                                                | `any`          | `{}`                                                        |    no    |
| <a name="input_external_secrets_kms_key_arns"></a> [external_secrets_kms_key_arns](#input_external_secrets_kms_key_arns)                                              | List of KMS Key ARNs that are used by Secrets Manager that contain secrets to mount using External Secrets                  | `list(string)` | <pre>[<br> "arn:aws:kms:*:*:key/*"<br>]</pre>               |    no    |
| <a name="input_external_secrets_secrets_manager_arns"></a> [external_secrets_secrets_manager_arns](#input_external_secrets_secrets_manager_arns)                      | List of Secrets Manager ARNs that contain secrets to mount using External Secrets                                           | `list(string)` | <pre>[<br> "arn:aws:secretsmanager:*:*:secret:*"<br>]</pre> |    no    |
| <a name="input_external_secrets_ssm_parameter_arns"></a> [external_secrets_ssm_parameter_arns](#input_external_secrets_ssm_parameter_arns)                            | List of Systems Manager Parameter ARNs that contain secrets to mount using External Secrets                                 | `list(string)` | <pre>[<br> "arn:aws:ssm:*:*:parameter/*"<br>]</pre>         |    no    |
| <a name="input_fargate_fluentbit"></a> [fargate_fluentbit](#input_fargate_fluentbit)                                                                                  | Fargate fluentbit add-on config                                                                                             | `any`          | `{}`                                                        |    no    |
| <a name="input_fargate_fluentbit_cw_log_group"></a> [fargate_fluentbit_cw_log_group](#input_fargate_fluentbit_cw_log_group)                                           | AWS Fargate Fluentbit CloudWatch Log Group configurations                                                                   | `any`          | `{}`                                                        |    no    |
| <a name="input_gatekeeper"></a> [gatekeeper](#input_gatekeeper)                                                                                                       | Gatekeeper add-on configuration                                                                                             | `any`          | `{}`                                                        |    no    |
| <a name="input_helm_releases"></a> [helm_releases](#input_helm_releases)                                                                                              | A map of Helm releases to create. This provides the ability to pass in an arbitrary map of Helm chart definitions to create | `any`          | `{}`                                                        |    no    |
| <a name="input_ingress_nginx"></a> [ingress_nginx](#input_ingress_nginx)                                                                                              | Ingress Nginx add-on configurations                                                                                         | `any`          | `{}`                                                        |    no    |
| <a name="input_karpenter"></a> [karpenter](#input_karpenter)                                                                                                          | Karpenter add-on configuration values                                                                                       | `any`          | `{}`                                                        |    no    |
| <a name="input_karpenter_enable_spot_termination"></a> [karpenter_enable_spot_termination](#input_karpenter_enable_spot_termination)                                  | Determines whether to enable native node termination handling                                                               | `bool`         | `true`                                                      |    no    |
| <a name="input_karpenter_node"></a> [karpenter_node](#input_karpenter_node)                                                                                           | Karpenter IAM role and IAM instance profile configuration values                                                            | `any`          | `{}`                                                        |    no    |
| <a name="input_karpenter_sqs"></a> [karpenter_sqs](#input_karpenter_sqs)                                                                                              | Karpenter SQS queue for native node termination handling configuration values                                               | `any`          | `{}`                                                        |    no    |
| <a name="input_kube_prometheus_stack"></a> [kube_prometheus_stack](#input_kube_prometheus_stack)                                                                      | Kube Prometheus Stack add-on configurations                                                                                 | `any`          | `{}`                                                        |    no    |
| <a name="input_metrics_server"></a> [metrics_server](#input_metrics_server)                                                                                           | Metrics Server add-on configurations                                                                                        | `any`          | `{}`                                                        |    no    |
| <a name="input_oidc_provider_arn"></a> [oidc_provider_arn](#input_oidc_provider_arn)                                                                                  | The ARN of the cluster OIDC Provider                                                                                        | `string`       | n/a                                                         |   yes    |
| <a name="input_secrets_store_csi_driver"></a> [secrets_store_csi_driver](#input_secrets_store_csi_driver)                                                             | CSI Secrets Store Provider add-on configurations                                                                            | `any`          | `{}`                                                        |    no    |
| <a name="input_secrets_store_csi_driver_provider_aws"></a> [secrets_store_csi_driver_provider_aws](#input_secrets_store_csi_driver_provider_aws)                      | CSI Secrets Store Provider add-on configurations                                                                            | `any`          | `{}`                                                        |    no    |
| <a name="input_tags"></a> [tags](#input_tags)                                                                                                                         | A map of tags to add to all resources                                                                                       | `map(string)`  | `{}`                                                        |    no    |
| <a name="input_velero"></a> [velero](#input_velero)                                                                                                                   | Velero add-on configuration values                                                                                          | `any`          | `{}`                                                        |    no    |
| <a name="input_vpa"></a> [vpa](#input_vpa)                                                                                                                            | Vertical Pod Autoscaler add-on configuration values                                                                         | `any`          | `{}`                                                        |    no    |

## Outputs

| Name                                                                                                                                               | Description                                               |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| <a name="output_argo_events"></a> [argo_events](#output_argo_events)                                                                               | Map of attributes of the Helm release created             |
| <a name="output_argo_rollouts"></a> [argo_rollouts](#output_argo_rollouts)                                                                         | Map of attributes of the Helm release created             |
| <a name="output_argo_workflows"></a> [argo_workflows](#output_argo_workflows)                                                                      | Map of attributes of the Helm release created             |
| <a name="output_argocd"></a> [argocd](#output_argocd)                                                                                              | Map of attributes of the Helm release created             |
| <a name="output_aws_cloudwatch_metrics"></a> [aws_cloudwatch_metrics](#output_aws_cloudwatch_metrics)                                              | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_efs_csi_driver"></a> [aws_efs_csi_driver](#output_aws_efs_csi_driver)                                                          | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_for_fluentbit"></a> [aws_for_fluentbit](#output_aws_for_fluentbit)                                                             | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_fsx_csi_driver"></a> [aws_fsx_csi_driver](#output_aws_fsx_csi_driver)                                                          | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_gateway_api_controller"></a> [aws_gateway_api_controller](#output_aws_gateway_api_controller)                                  | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_load_balancer_controller"></a> [aws_load_balancer_controller](#output_aws_load_balancer_controller)                            | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_node_termination_handler"></a> [aws_node_termination_handler](#output_aws_node_termination_handler)                            | Map of attributes of the Helm release and IRSA created    |
| <a name="output_aws_privateca_issuer"></a> [aws_privateca_issuer](#output_aws_privateca_issuer)                                                    | Map of attributes of the Helm release and IRSA created    |
| <a name="output_cert_manager"></a> [cert_manager](#output_cert_manager)                                                                            | Map of attributes of the Helm release and IRSA created    |
| <a name="output_cluster_autoscaler"></a> [cluster_autoscaler](#output_cluster_autoscaler)                                                          | Map of attributes of the Helm release and IRSA created    |
| <a name="output_cluster_proportional_autoscaler"></a> [cluster_proportional_autoscaler](#output_cluster_proportional_autoscaler)                   | Map of attributes of the Helm release and IRSA created    |
| <a name="output_eks_addons"></a> [eks_addons](#output_eks_addons)                                                                                  | Map of attributes for each EKS addons enabled             |
| <a name="output_external_dns"></a> [external_dns](#output_external_dns)                                                                            | Map of attributes of the Helm release and IRSA created    |
| <a name="output_external_secrets"></a> [external_secrets](#output_external_secrets)                                                                | Map of attributes of the Helm release and IRSA created    |
| <a name="output_fargate_fluentbit"></a> [fargate_fluentbit](#output_fargate_fluentbit)                                                             | Map of attributes of the configmap and IAM policy created |
| <a name="output_gatekeeper"></a> [gatekeeper](#output_gatekeeper)                                                                                  | Map of attributes of the Helm release and IRSA created    |
| <a name="output_helm_releases"></a> [helm_releases](#output_helm_releases)                                                                         | Map of attributes of the Helm release created             |
| <a name="output_ingress_nginx"></a> [ingress_nginx](#output_ingress_nginx)                                                                         | Map of attributes of the Helm release and IRSA created    |
| <a name="output_karpenter"></a> [karpenter](#output_karpenter)                                                                                     | Map of attributes of the Helm release and IRSA created    |
| <a name="output_kube_prometheus_stack"></a> [kube_prometheus_stack](#output_kube_prometheus_stack)                                                 | Map of attributes of the Helm release and IRSA created    |
| <a name="output_metrics_server"></a> [metrics_server](#output_metrics_server)                                                                      | Map of attributes of the Helm release and IRSA created    |
| <a name="output_secrets_store_csi_driver"></a> [secrets_store_csi_driver](#output_secrets_store_csi_driver)                                        | Map of attributes of the Helm release and IRSA created    |
| <a name="output_secrets_store_csi_driver_provider_aws"></a> [secrets_store_csi_driver_provider_aws](#output_secrets_store_csi_driver_provider_aws) | Map of attributes of the Helm release and IRSA created    |
| <a name="output_velero"></a> [velero](#output_velero)                                                                                              | Map of attributes of the Helm release and IRSA created    |
| <a name="output_vpa"></a> [vpa](#output_vpa)                                                                                                       | Map of attributes of the Helm release and IRSA created    |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

Starting with [EKS Blueprints v5](https://github.com/aws-ia/terraform-aws-eks-blueprints/blob/main/docs/v4-to-v5/motivation.md) we have made a decision to only support the provisioning of a certain core set of [add-ons](./addons/). On an going basis, we will evaluate the current list to see if more add-ons need to be supported via this repo. Typically you can expect that any AWS created add-on that is not yet available via the [Amazon EKS add-ons](./amazon-eks-addons.md) will be prioritized to be provisioned through this repository.

In addition to these AWS add-ons, we will also support the provisioning of certain OSS add-ons that we think customers will benefit from. These are selected based on customer demand (e.g. [metrics-server](./addons/metrics-server.md)) and certain patterns ([gitops](./addons/argocd.md)) that are foundational elements for a complete blueprint of an EKS cluster.

One of the reasons customers pick Kubernetes is because of its strong commercial and open-source software ecosystem and would like to provision add-ons that are not necessarily supported by EKS Blueprints. For such add-ons the options are as following:

## With `helm_release` Terraform Resource

The [helm_release](https://registry.terraform.io/providers/hashicorp/helm/latest/docs/resources/release) resource is the most fundamental way to provision a helm chart via Terraform.

Use this resource, if you need to control the lifecycle add-ons down to level of each add-on resource.

## With `helm_releases` Variable

You can use the `helm_releases` variable in [EKS Blueprints Add-ons](https://registry.terraform.io/modules/aws-ia/eks-blueprints-addons/aws/latest?tab=inputs) to provide a map of add-ons and their respective Helm configuration. Under the hood, we just iterate through the provided map and pass each configuration to the Terraform [helm_release](https://registry.terraform.io/providers/hashicorp/helm/latest/docs/resources/release) resource.

E.g.

```hcl
module "addons" {
  source  = "aws-ia/eks-blueprints-addons/aws"
  version = "~> 1.0"

  cluster_name      = "<cluster_name>"
  cluster_endpoint  = "<cluster_endpoint>"
  cluster_version   = "<cluster_version>"
  oidc_provider_arn = "<oidc_provider_arn>"

  # EKS add-ons
  eks_addons = {
    coredns = {}
    vpc-cni = {}
    kube-proxy = {}
  }

  # Blueprints add-ons
  enable_aws_efs_csi_driver                    = true
  enable_aws_cloudwatch_metrics                = true
  enable_cert_manager                          = true
  ...

  # Pass in any number of Helm charts to be created for those that are not natively supported
  helm_releases = {
    prometheus-adapter = {
      description      = "A Helm chart for k8s prometheus adapter"
      namespace        = "prometheus-adapter"
      create_namespace = true
      chart            = "prometheus-adapter"
      chart_version    = "4.2.0"
      repository       = "https://prometheus-community.github.io/helm-charts"
      values = [
        <<-EOT
          replicas: 2
          podDisruptionBudget:
            enabled: true
        EOT
      ]
    }
    gpu-operator = {
      description      = "A Helm chart for NVIDIA GPU operator"
      namespace        = "gpu-operator"
      create_namespace = true
      chart            = "gpu-operator"
      chart_version    = "v23.3.2"
      repository       = "https://nvidia.github.io/gpu-operator"
      values = [
        <<-EOT
          operator:
            defaultRuntime: containerd
        EOT
      ]
    }
  }

  tags = local.tags
}
```

With this pattern, the lifecycle of all your add-ons is tied to that of the `addons` module. This allows you to easily target the addon module in your Terraform apply and destroy commands. E.g.

```sh
terraform apply -target=module.addons

terraform destroy -target=module.addons
```

## With EKS Blueprints Addon Module

If you have an add-on that requires an IAM Role for Service Account (IRSA), we have created a new Terraform module [terraform-aws-eks-blueprints-addon](https://registry.terraform.io/modules/aws-ia/eks-blueprints-addon/aws/latest) that can help provision a Helm chart along with an IAM role and policies with permissions required for the add-on to function properly. We use this module for all of the add-ons that are provisioned by EKS Blueprints Add-ons today.

You can optionally use this module for add-ons that do not need IRSA or even just to create the IAM resources for IRSA and skip the helm release. Detailed usage of how to consume this module can be found in its [readme](https://github.com/aws-ia/terraform-aws-eks-blueprints-addon#readme).

This pattern can be used to create a Terraform module with a set of add-ons that are not supported in the EKS Blueprints Add-ons today and wrap them in the same module definition. An example of this is the [ACK add-ons repository](https://github.com/aws-ia/terraform-aws-eks-ack-addons) which is a collection of ACK helm chart deployments with IRSA for each of the ACK controllers.
