In this project, the architecture will be initiated with a manually constructed single instance, with the application and database being run through the stages, gradually evolving it into a scalable and resilient architecture.

This project consists of 5 stages, each implementing additional components of the architecture

Stage 1 - Setup the environment and manually build wordpress
Stage 2 - Automate the build using a Launch Template
Stage 3 - Split out the DB into RDS and Update the LT
Stage 4 - Split out the WP filesystem into EFS and Update the LT
Stage 5 - Enable elasticity via a ASG & ALB and fix wordpress (hardcoded WPHOME)



