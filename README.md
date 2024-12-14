# Cloud Connector Dashboard

A modern dashboard for managing cloud services across AWS, Azure, and GCP.

## Deployment Instructions

### Prerequisites
1. Python 3.9 or higher
2. Node.js 14 or higher
3. AWS Account with the following permissions:
   - S3 full access
   - CloudFront full access
   - Lambda full access
   - API Gateway full access
   - IAM role creation

### Step 1: Build the Frontend
```bash
# Install dependencies
npm install

# Build the production version
npm run build
```

### Step 2: Prepare the Backend
```bash
# Navigate to the api directory
cd api

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Configure AWS Credentials
1. Create an IAM role for Lambda with the following permissions:
   - AWSLambdaBasicExecutionRole
   - AmazonS3FullAccess
   - AmazonEC2FullAccess
   - CloudWatchFullAccess

2. Update the `deploy/deploy.py` script with:
   - Your AWS access key and secret
   - Your AWS account ID
   - The ARN of the Lambda role you created

### Step 4: Deploy
```bash
# Run the deployment script
python deploy/deploy.py
```

The script will:
1. Create an S3 bucket for the frontend
2. Upload the built Next.js files
3. Create a CloudFront distribution
4. Deploy the Flask API to Lambda
5. Create an API Gateway

### Step 5: Update API URL
Once deployment is complete, update the API URL in your frontend configuration:

1. Create a `.env.local` file in the root directory
2. Add the API Gateway URL:
```
NEXT_PUBLIC_API_URL=https://your-api-gateway-url.execute-api.us-east-1.amazonaws.com/prod
```

3. Rebuild and redeploy the frontend:
```bash
npm run build
python deploy/deploy.py
```

## Accessing the Dashboard
After deployment, you can access your dashboard at the CloudFront URL provided in the deployment output.

## Security Notes
- Make sure to keep your AWS credentials secure
- Consider using AWS Secrets Manager for sensitive values
- Enable CORS only for your frontend domain
- Set up proper IAM roles and permissions
- Consider adding authentication to your API 

## Environment Variables

The following environment variables are required:

### Azure Configuration
- `AZURE_SUBSCRIPTION_KEY`: Your Azure Cognitive Services subscription key
- `AZURE_SUBSCRIPTION_ID`: Your Azure subscription ID
- `AZURE_VM_USERNAME`: Username for Azure VM creation
- `AZURE_VM_PASSWORD`: Password for Azure VM creation

### GCP Configuration
- `GOOGLE_CLOUD_PROJECT`: Your Google Cloud project ID
- `GOOGLE_APPLICATION_CREDENTIALS`: Path to your Google Cloud service account key file

### AWS Configuration
- `AWS_ACCESS_KEY_ID`: Your AWS access key
- `AWS_SECRET_ACCESS_KEY`: Your AWS secret key
- `AWS_DEFAULT_REGION`: AWS region (defaults to us-east-1)

Make sure to create a `.env` file in the root directory with these variables before running the application. 