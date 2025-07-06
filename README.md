
# 🌐 GitShowcaseAPI

A full-stack, serverless web application to showcase GitHub developer profiles, including top repositories, total stars, commit counts, and real-time activity — all powered by the GitHub API and hosted entirely on AWS.

### 🚀 Live Demo  
🟢 Hosted via AWS CloudFront (CDN): [https://d3tbtv7bxs3vbw.cloudfront.net](https://d3tbtv7bxs3vbw.cloudfront.net)

---

## 🧩 Features

- 🔍 Register any GitHub username
- 🌟 Display top repositories sorted by stars
- 📊 Show total stars, commits, and public repositories
- ⏱️ Track recent GitHub activity (last seen date)
- 🔁 Hourly data refresh via AWS EventBridge
- 🖼️ Clean, responsive UI hosted on CDN


---

## 📦 Tech Stack

### Frontend

- HTML, CSS, JavaScript
- AWS S3 (static hosting)
- AWS CloudFront (CDN delivery)

### Backend

- AWS Lambda (compute)
  - `/register` — fetches and caches GitHub user data
  - `/showcase` — serves cached profile data
- AWS API Gateway (REST interface)
- AWS DynamoDB (data storage)
- AWS EventBridge (hourly refresh trigger)
- AWS Secrets Manager (secure API token storage)
- GitHub API (primary data source)

---

## 🔄 CI/CD Deployment

Every push to the `main` branch triggers a GitHub Actions workflow that:

- Invokes a deployment Lambda function
- Pulls the latest frontend from GitHub
- Uploads it to the S3 bucket
- Invalidates CloudFront cache for immediate update

> GitHub secrets must include your AWS access credentials (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).

---

## 🧠 AWS Architecture Overview

- **CloudFront** serves the frontend globally via CDN
- **S3** stores static frontend files
- **GitHub Actions** triggers deployments via Lambda
- **API Gateway** routes HTTP calls to backend Lambdas
- **Lambda Functions** handle user registration and profile data retrieval
- **DynamoDB** stores and caches user/repo data
- **EventBridge** runs scheduled data refresh tasks
- **Secrets Manager** secures your GitHub API token

---

## 🧪 Sample Output

```
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
```

## 🧪 Sample Input   

```
POST /register
{
  "username": "octocat"
}
```

---
🧠 AWS Architecture Diagram

![GitShowCaseAPI](https://github.com/user-attachments/assets/54aa061a-7444-4c19-937f-47720299ea4c)

   ---

## 🌱 Future Enhancements

- 🌈 Migrate frontend to React or Next.js
- 📈 Add GitHub-style contribution heatmaps
- 🔍 Repo filtering and advanced search
- 🧪 Add unit tests for Lambda logic
- 🪄 Slack/Discord bot integration for profile sharing

---

## 🙌 Author & Credits

Built by **Kartikey Pandey** and **Ritika Sharma** with 💻 and ☕.  
Special thanks to **GitHub** and **AWS** for their APIs and infrastructure.

---

## 📄 License

**MIT License** — Free to use, with credit appreciated.


