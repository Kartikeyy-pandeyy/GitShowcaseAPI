GitShowcaseAPI 🌐
A full-stack, serverless web app to showcase GitHub developer profiles — with top repositories, stars, commits, and real-time activity — built entirely on AWS and the GitHub API.

🚀 Live Demo
🟢 Live at: CloudFront Distribution

🧩 Features

🔍 Register any GitHub username
🌟 Display top repositories by stars
📊 Show total stars, commits, and public repositories
⏱️ Track recent GitHub activity (last seen date)
🔁 Hourly data refresh with AWS EventBridge
🖼️ Clean, responsive static frontend deployed via CDN


📦 Tech Stack
🖥️ Frontend

HTML, CSS, JavaScript
Hosted on AWS S3
Delivered through AWS CloudFront

⚙️ Backend

AWS Lambda — serverless compute:
/register: Fetches GitHub user data and stores it
/showcase: Serves stored profile data


AWS API Gateway — RESTful interface for Lambda
AWS DynamoDB — Stores user metadata and cache
AWS EventBridge — Triggers automatic hourly updates
AWS Secrets Manager — Safely stores GitHub API token
GitHub API — Primary data source


🔄 CI/CD Deployment (Lambda + S3)
✅ Automated Deployment on Push
Every push to the main branch triggers a GitHub Actions workflow that:

Invokes an AWS Lambda function
Downloads the latest frontend files from GitHub
Uploads them to your S3 bucket
Invalidates the CloudFront cache to reflect changes instantly

📁 Workflow File: .github/workflows/deploy.yml
name: Deploy to S3 via Lambda

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v3

    - name: Invoke Deployment Lambda Function
      env:
        AWS_REGION: us-east-1
        FUNCTION_NAME: GitShowcaseFrontendDeployer
      run: |
        aws lambda invoke \
          --function-name "$FUNCTION_NAME" \
          --region "$AWS_REGION" \
          --payload '{}' \
          response.json

    - name: Show Lambda Response
      run: cat response.json


📌 Make sure your GitHub repository has AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY stored as secrets.


📂 Repository Structure
├── index.html             # Main UI
├── script.js              # Frontend logic
├── style.css              # Custom styling
├── .github/
│   └── workflows/
│       └── deploy.yml     # CI/CD GitHub Action
├── lambda/
│   └── deploy_function.py # AWS Lambda source (for S3 deploy + CF invalidation)


📸 Screenshots

(Add preview images of your UI here)Example: Homepage, user showcase, responsive view, etc.


🛠️ Local Development

Clone the repository:
git clone https://github.com/yourusername/gitshowcaseapi.git
cd gitshowcaseapi


Open index.html in a browser.



🧠 AWS Architecture Diagram
+---------------------+
|     CloudFront      |
| (CDN Distribution)  |
+---------+-----------+
          |
          v
     +----+----+             +-----------------+
     |   S3     |<-----------| GitHub Repo     |
     | (Static  |   Deploys  | via Lambda CI/CD|
     | Frontend)|            +-----------------+
          |
          v
   +------+--------+
   |  API Gateway  |
   +------+--------+
          |
  +-------+--------+
  |    Lambda       |
  |  /register      |
  |  /showcase      |
  +-------+--------+
          |
          v
      DynamoDB
          ^
          |
     EventBridge
   (Hourly Trigger)


🧪 Example Showcase Output
{
  "username": "octocat",
  "name": "The Octocat",
  "avatar_url": "https://avatars.githubusercontent.com/u/583231?v=4",
  "bio": "This is a GitHub bio",
  "top_repos": [
    {
      "name": "cool-project",
      "stars": 120,
      "forks": 30,
      "url": "https://github.com/octocat/cool-project",
      "commits": 42
    }
  ],
  "total_stars": 340,
  "total_commits": 523,
  "total_repos": 10,
  "last_seen": "2024-05-04T15:21:33Z"
}


🧠 Future Enhancements

🌈 Upgrade frontend to React or Next.js
📈 Visual contribution graphs (GitHub heatmaps)
🔍 Public repo search + filters
🧪 Add tests to Lambda functions
🪄 Slack/Discord bot integration to display profiles


🙌 Author & Credits
Built with 💻 and ☕ by Your NameSpecial thanks to GitHub, AWS, and OpenAI for the tools and APIs.

📄 License
MIT License – Use freely, credit appreciated.
