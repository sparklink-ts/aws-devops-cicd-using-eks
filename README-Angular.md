***Angular Based Frontend Deployments***

To deploy an Angular application using AWS CodePipeline, the standard approach is to use Amazon S3 for static website hosting or Amazon EC2 with CodeDeploy for server-side rendering or more complex setups. The S3 method is typically more cost-effective and scalable for standard Angular single-page applications (SPAs). 
Core AWS Services Involved 

• AWS S3: Used for hosting the static Angular application files. 
• AWS CodeCommit/GitHub: Source control repository for your application code. 
• AWS CodeBuild: Compiles the Angular application into production-ready files ( folder) using a  file. 
• AWS CodePipeline: Orchestrates the entire Continuous Integration/Continuous Deployment (CI/CD) process from code commit to deployment. 
• AWS CloudFront (Recommended): A Content Delivery Network (CDN) that provides better performance, HTTPS support, and caching for the S3-hosted app. 

Step-by-Step Deployment (S3 and CodePipeline)
The following steps outline how to set up an automated CI/CD pipeline: 

1. Prepare the Angular App and Source Control 

	• Create your Angular application and push the code to a  GitHub 
 or AWS CodeCommit repository. 
	• Include a  file in the root directory of your project. This file contains instructions for AWS CodeBuild. 

2. An example  for an Angular app might look like this: 
3. Set Up AWS S3 for Static Website Hosting 

	• Create a new S3 bucket in the  AWS Management Console 
. 
	• Disable "Block all public access" settings for the bucket (or use CloudFront OAI for better security). 
	• In the Properties tab, enable Static website hosting, setting  as both the Index and Error document. 
	• In the Permissions tab, add a bucket policy to allow public read access (if not using CloudFront OAI). 

4. Create the AWS CodePipeline 

	• Navigate to the  AWS CodePipeline console 
 and select Create pipeline. 
	• Pipeline settings: Give your pipeline a name and allow AWS to create a new service role. 
	• Source stage: Select your source provider (e.g.,  GitHub 
), connect your account, and choose your repository and branch. 
	• Build stage: 

		• Select AWS CodeBuild as the build provider. 
		• Choose Create project to define the build environment (e.g., Ubuntu, Standard runtime, latest image). 
		• Select Use a buildspec file to use the  you added to your repository. 

	• Deploy stage: 

		• Select Amazon S3 as the deploy provider. 
		• Choose the S3 bucket you created earlier. 
		• Check the box for "Extract file before deploy" to ensure the build artifacts are correctly placed in the bucket. 

	• Review and Create: Review your configuration and create the pipeline. The pipeline will automatically start its first execution. 

Once the pipeline successfully runs, your Angular application will be accessible via the S3 bucket's website endpoint URL. Any future code pushes to your source repository will automatically trigger a new build and deployment cycle, automating your release process. 


