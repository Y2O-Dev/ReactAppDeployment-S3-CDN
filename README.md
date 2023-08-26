# Automate Node.js Build, Deployment, and CloudFront Cache Invalidation with AWS CodePipeline


 ## Step 1: Set Up the Web App ## 
1. To set up the Node.js web application, use the command:
   
   ` npx create-react-app my-node-app`

   This command initializes a new React application in a directory named "my-node-app."

## Step 2: Verify Local Functionality ##
1. Validate the app's local functionality by running the following commands:
   - To start the development server:
     
     ` npm start`

     This command launches the development server, which enable viewing the app in a local environment.
   - To build the app for production:

   ![autostart-node-app](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/ed987185-9b3f-4827-9f3e-acc2cf2b3565)
     
     ` npm run build `
     Running this command generates a production-ready build of the app that can be deployed.

    ![run-build](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/146c4041-ffe0-46ba-ae95-32886916b4c5)

    ---
 ## Step 3: Install and Configure AWS CLI ## 

1. Install the AWS Command Line Interface (CLI) on the Ubuntu local system using the package manager:
   - Open a terminal.
   - Run the following command to install the AWS CLI:

     ` sudo apt install awscli `
   - Verify the installation by checking the version:
    
     ` aws --version `

2. Configure the AWS CLI by running:
   
   ` aws configure `
   
   This command prompts for the AWS access key, secret key, default region, and output format.

   ![awscli-config-credentials](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/1baedf32-7eb5-4284-8d61-46be6023f6bb)

   ---

 ## Step 4: Configure Git and Push to GitHub ## 
1. Set up Git and push the code to GitHub as follows:
   - Initialize Git repository:
     `git init `

   - Add the files to the staging area:
     `git add . `

   - Commit the changes:
     ` git commit -m "Initial commit" `

   - Connect the local repository to the GitHub repository:
     ` git remote add origin https://github.com/the-username/repo-name.git `

   - Push the code to GitHub:
     ` git push -u origin master `

 ## Step 5: Create an S3 Bucket ## 
- Use the AWS Management Console to create an S3 bucket:
   - Log in to the console and navigate to Amazon S3.
   - Click the "Create bucket" button.
   - Provide a unique bucket name (e.g., "BB") and choose region and other settings as needed.

   ![s3-bucket](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/15909d80-62ad-46c9-a932-074dbdc2050c)

   ---

 ## Step 6: Set Up CloudFront Distribution ## 
- Create a CloudFront distribution through the AWS Management Console:

   - Navigate to Amazon CloudFront.
   - Click the "Create Distribution" button.
   - Select "Web" as the delivery method.
   - Specify the created S3 bucket as the origin domain name.
   - Configure other settings and distribution options as required.

 ## Step 7: Create an AWS CodePipeline ## 
- Set up an AWS CodePipeline to automate the deployment process:

   - Access the AWS Management Console.

   - Navigate to AWS CodePipeline.
   
   - Click the "Create pipeline" button.
   
   - Configure the source stage to connect to the GitHub repository.
   
   - Configure the build stage to use AWS CodeBuild:
     - Specify the buildspec file.
     - Set the runtime version to Node.js 18.

   - Configure the deploy stage to use AWS CodeDeploy:
     - Specify the "BB" S3 bucket as the deployment destination.
     - Enter the CloudFront distribution ID to trigger cache invalidation.
     
   - Configure IAM role to grant the build access permission to s3, Cloud front.
      
      ![role](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/1ad3d52a-5c26-425e-bfa3-34275a66cf80)

    ---

 ## Step 8: Pipeline Execution and Deployment ## 
1. Once the AWS CodePipeline is configured, it will automatically trigger upon changes in the GitHub repository.

2. The pipeline will execute the following phases:
   - Source: Clone the repository and fetch the source code.
   - Build: Use the buildspec file to run the build process.
   - Deploy: Deploy the build artifacts to the "BB" S3 bucket.
   - CloudFront Invalidation: Invalidate CloudFront cache to ensure fresh content.

   ![pipeline](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/9f871a4e-cb1a-4090-aea3-835a03d50aa0)
    ---
   ![s3-contents](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/6c21260b-96b1-40a2-b3f7-c6a8e5004a10)
    ---

- Bucket populated after executing the pipeline

   ![cloudfront-url](https://github.com/Y2O-Dev/ReactAppDeployment-S3-CDN/assets/114786664/d7ae2763-9862-4df1-97da-16088f934cff)

   ---
   END