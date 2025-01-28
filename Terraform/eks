module "eks" {
    source = "terraform-aws-modules/eks/aws"
    version = "20.33.1"
    cluster_name = local.cluster_name
    cluster_version = var.kubernetes_version
    subnet_ids = module.vpc.private_subnets

    enable_irsa = true

    tags = {

        cluster = "project"
        
    }
    cluster_endpoint_public_access = true

    vpc_id = module.vpc.vpc_id
    

    eks_managed_node_group_defaults = {

        ami_type  = "AL2_x86_64"
        ami_image = "ami-08f0763ca70b0be4c"
        instance_types = ["t3.medium"]
        vpc_security_group_ids = [aws_security_group.sun_sg.id] 
        associate_public_ip_address = true
        
                
    }

   
   eks_managed_node_groups = {


     node_group = {
       min_size   =   2
       max_size   =   4
       desired_size = 2 

     } 
   }

  
}
