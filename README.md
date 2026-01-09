# backups-my-firestore-to-Cloud-Storage
Firebase extension for scheduled Firestore backups to Cloud Storage
# 🔁 Firestore Scheduled Backup Extension

This Firebase Extension automatically exports your Firestore database to a Cloud Storage bucket on a schedule.  
It supports **Node.js 20 / Cloud Functions 2nd Gen** and avoids the Node.js 18 runtime issue.

---

## ✨ Features
- Scheduled backups using cron syntax (e.g., quarterly, monthly).
- Exports **all collections** or only specified ones.
- Stores backups in Cloud Storage with timestamped folder names.
- Retries automatically if a path collision occurs.
- Works across multiple Firebase projects.

---

## 📦 Installation

### 1. Install from GitHub
From your Firebase project root, run:

```bash
firebase ext:install <your-username>/backup-firestore-to-storage
Replace <your-username> with your GitHub handle.
2. Configure Parameters
During installation you’ll be prompted for:
- BUCKET_NAME → Cloud Storage bucket (e.g., my-backup-bucket)
- PREFIX_PATH → Optional folder prefix (default: firestore-backup)
- COLLECTION_IDS → Comma‑separated list of collections (leave blank for all)
- SCHEDULE → Cron schedule (default: 0 0 1 */3 * → quarterly)
- TIME_ZONE → Time zone (default: UTC)
- TIMESTAMP_FORMAT → Format for folder names (default: yyyy-MM-dd'T'HH:mm:ss)
- LOCATION → Cloud Functions region (e.g., europe-west2)

🛠️ Example Configurations
Quarterly backup of all collections
- BUCKET_NAME: project-backups
- COLLECTION_IDS: (leave blank)
- SCHEDULE: 0 0 1 */3 *
- TIME_ZONE: UTC
Monthly backup of selected collections
- BUCKET_NAME: project-backups
- COLLECTION_IDS: users,posts
- SCHEDULE: 0 0 1 * *
- TIME_ZONE: UTC

🔧 Development Notes
- Runtime: Node.js 20
- Cloud Functions: 2nd Gen
- IAM roles required:
- Firestore Admin (to export documents)
- Storage Admin (to write to bucket)

🚀 Deploying Updates
If you make changes to the extension code:
git add .
git commit -m "Update backup logic"
git push origin main

Then reinstall or update the extension in your Firebase project:

firebase ext:update <your-username>/backup-firestore-to-storage
