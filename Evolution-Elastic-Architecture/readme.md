In this project, the architecture will be initiated with a manually constructed single instance, with the application and database being run through the stages, gradually evolving it into a scalable and resilient architecture.

This project consists of 5 stages, each implementing additional components of the architecture

Stage 1 - Setup the environment and manually build wordpress

Stage 2 - Automate the build using a Launch Template

Stage 3 - Split out the DB into RDS and Update the LT

Stage 4 - Split out the WP filesystem into EFS and Update the LT

Stage 5 - Enable elasticity via a ASG & ALB and fix wordpress (hardcoded WPHOME)


## Instructions

- [Stage 1](https://github.com/sunjeevs/AWS-Projects/blob/main/Evolution-Elastic-Architecture/Stages/Stage%201%20-%20Setup%20and%20Manual%20Wordpress%20Build.md)
- [Stage 2](https://github.com/acantril/learn-cantrill-io-labs/blob/master/aws-elastic-wordpress-evolution/02_LABINSTRUCTIONS/STAGE2%20-%20Automate%20the%20build%20using%20a%20Launch%20Template.md)
- [Stage 3](https://github.com/acantril/learn-cantrill-io-labs/blob/master/aws-elastic-wordpress-evolution/02_LABINSTRUCTIONS/STAGE3%20-%20Add%20RDS%20and%20Update%20the%20LT.md)
- [Stage 4](https://github.com/acantril/learn-cantrill-io-labs/blob/master/aws-elastic-wordpress-evolution/02_LABINSTRUCTIONS/STAGE4%20-%20Add%20EFS%20and%20Update%20the%20LT.md)
- [Stage 5](https://github.com/acantril/learn-cantrill-io-labs/blob/master/aws-elastic-wordpress-evolution/02_LABINSTRUCTIONS/STAGE5%20-%20Add%20an%20ELB%20and%20ASG.md)
- [Stage 6](https://github.com/acantril/learn-cantrill-io-labs/blob/master/aws-elastic-wordpress-evolution/02_LABINSTRUCTIONS/STAGE6%20-%20CLEANUP.md)


