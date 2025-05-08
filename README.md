# GitShowcaseAPI 🌐

A full-stack serverless web app to showcase GitHub developer profiles — including top repositories, total stars, commits, and activity — powered by AWS and the GitHub API.

## 🚀 Live Demo

Visit: [gitshowcaseapi.work.gd](https://d3tbtv7bxs3vbw.cloudfront.net)

---

## 🧩 Features

- 🔍 Register any GitHub username
- 🌟 Show top repositories by stars
- 🧮 Track total stars, commits, repos
- ⏱️ See last activity date
- 🔁 Background data refresh every hour (via AWS EventBridge)
- 🖼️ Clean and responsive frontend

---

## 📦 Tech Stack

### Frontend

- HTML + CSS + JS
- Hosted on AWS S3
- Delivered via AWS CloudFront CDN

### Backend

- **AWS API Gateway** – public REST API endpoints
- **AWS Lambda** – serverless compute for:
  - `/register` – fetches and stores GitHub data
  - `/showcase` – retrieves stored data
- **AWS DynamoDB** – persistent GitHub user data storage
- **AWS EventBridge** – schedules hourly GitHub data refresh
- **GitHub API** – source of public GitHub profile data

---

## 📸 Screenshots

> _You can add screenshots of the live site here_

---

## 🛠️ Local Development

To run locally:

1. Clone the repo:
   ```bash
   git clone https://github.com/yourusername/gitshowcaseapi.git
   cd gitshowcaseapi
   ```

2. Open `index.html` in your browser.

---

## 🔧 AWS Architecture Overview

```plaintext
GitHub User -> Frontend (S3/CloudFront) -> API Gateway
                ↘︎                         ↙︎
                 Lambda (/register, /showcase)
                        ↕
                    DynamoDB
                        ⬆
              EventBridge (Hourly Trigger)
```

---

## 🧪 Example Output

```json
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

---

## 🧠 Future Enhancements

- 🌈 UI redesign with Tailwind or React
- 🧾 GitHub contribution graph
- 🗂️ Filtering and searching public repos
- 🧪 Unit testing Lambda functions

---

## 🙌 Credits

Built with 💻 by [Your Name]

---

## 📄 License

MIT
